
```javascript
const Book = types.model({
    title: types.string,
    price: types.number
}, {
    setPrice(newPrice) {
        this.price = newPrice
    }
})
```

```javascript
const store = Store.create({
    books: [{
        title:
            "The Hidden Life of Trees: What They Feel, How They Communicate",
        price: 24.95
    }]
})
```

```javascript
store.books.push(Book.create({ title: "A Tree Grows in Brooklyn" }))
```

```javascript
const store = Store.create({
    books: [{
        price: "24.95"
    }]
})
```

```javascript
const Book = types.model({
    title: types.string,
    price: types.number
}, {
    setPrice(newPrice) {
        this.price = newPrice
    }
})
```

```javascript
store.books[0].title = "I hate trees!"
```

```javascript
import { clone, recordActions } from "mobx-state-tree"
const bookCopy = clone(store.books[0])
```

```javascript
import { clone, recordActions } from "mobx-state-tree"
const bookCopy = clone(store)
const recorder = recordActions(bookCopy)
```

```javascript
function printPrice(book: Book) {
    setTimeout(
        () => console.log(book.price),
        1000
    )
}
printPrice(store.books.get("ISBN-123"))
```

```javascript
function printPrice(book: Book) {
    setTimeout(
        () => console.log(book.price),
        1000
    )
}
printPrice(store.books.get("ISBN-123"))
```

```javascript
function printPrice(book: Book) {
    setTimeout(
        () => console.log(book.price),
        1000
    )
}

printPrice(store.books.get("ISBN-123"))

printPrice(getSnapshot(store.books.get("ISBN-123")))
```

```javascript
printPrice(store.books.get("ISBN-123"))
store.removeBook("ISBN-123")
// what will be printed?
```

```
bookStore
   - books
       - book A
       - book B
   - cart
       - entry 1
           - book A ?
           - quantity
       - entry 2
           - book B ?
           - quantity
```          

```javascript
const CartEntry = types.model({
    amount: types.number,
    book: types.reference(Book)
})
cartEntry.book = bookStore.books[0]
console.log(bookEntry.book.title) // OK
console.dir(getSnapshot(bookEntry))
```

```javascript
import { types } from 'mobx-state-tree'
const Todo = types.model({
    text: 'Learn Redux',
    completed: false,
    id: 0
})
const TodoStore = types.model({
    todos: types.array(Todo),
    findTodoById: function (id) {
      return this.todos.find(todo => todo.id === id)
    }
}, {
    DELETE_TODO({id}) {
      this.todos.remove(this.findTodoById(id))
    }
    // .. and more
})
```
