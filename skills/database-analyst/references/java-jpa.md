# Java / Spring Data JPA Analysis

## 1. N+1 Query Detection

The "N+1 problem" occurs when an application loads a collection of N objects and then performs a separate query for each object to fetch related data.

### Detection
- Look for `@OneToMany` or `@ManyToMany` relationships with `FetchType.EAGER` (bad practice) or `LAZY` (default, but risky if accessed in a loop).
- Check repository methods. Standard `findAll()` does not fetch associations.
- Review Service logic:
  ```java
  List<Author> authors = authorRepository.findAll(); // Query 1
  for (Author a : authors) {
      a.getBooks().size(); // Query N (one per author)
  }
  ```

### Solutions
- **Entity Graph:** Use `@EntityGraph` on repository methods to fetch associations in a single query.
- **Join Fetch:** Use JPQL `JOIN FETCH`.
  ```java
  @Query("SELECT a FROM Author a JOIN FETCH a.books")
  List<Author> findAllWithBooks();
  ```

## 2. Transaction Management

- **@Transactional:** Ensure service methods modifying data are annotated.
- **Read-Only:** Use `@Transactional(readOnly = true)` for fetch-only operations to allow DB optimizations (e.g., avoiding dirty checking in Hibernate).
- **Boundaries:** Be aware that `@Transactional` only works on *external* method calls. Calling a transactional method from within the same class (using `this.method()`) bypasses the proxy and the transaction.

## 3. Repository Best Practices

- **Pagination:** Ensure large result sets use `Pageable` instead of returning `List<?>`.
- **Projections:** Use Interfaces or DTOs (Records) for read-only views to avoid fetching entire Entities when only a few columns are needed.
  ```java
  // Efficient
  List<UserNameOnly> findByActiveTrue();
  ```
