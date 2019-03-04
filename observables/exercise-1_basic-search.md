## Lab 1: Write a basic search implementation

The goal of this exercise is to write a first basic implementation of an instant search.

![o1](https://user-images.githubusercontent.com/210413/46899916-741af300-cef6-11e8-9c24-d055e447b798.jpg)


## Scenario

In `src/app/contacts-list/contacts-list.component.html` you already have the proper markup to render a list of contacts. The goal is to reuse the existing markup and add a search field on top of the list to implement the search feature.

## Tasks

1. Add a `ContactsService::search(term: string)` method to use the REST endpoint `http://localhost:4201/api/search?text=${term}`; where the `${term}` is the value of the **search** `term` argument.
2. Implement a `search()` method on `ContactsListComponent` which uses `ContactsService#search()`
>  Note: Change the ContactsListComponent variable to `contacts$` since the `search()` will return an `Observable<Array<Contact>>`.
3. Add a search field to `ContactsListComponent`'s template... on top of the contacts list. Here's a snippet:

  ```html
  <mat-toolbar>
    <mat-form-field color="accent" class="trm-search-container">
      <input matInput type="text" (input)="search($event.target.value)">
    </mat-form-field>
    <mat-icon color="accent">search</mat-icon>
  </mat-toolbar>
  ```
4. When the input control fires an `input` event, invoke the component's search logic; access and pass the input's value to the event handler.


## Code Snippets


###### `contacts.service.ts`

```ts
@Injectable()
export class ContactsService {
  constructor(private http: HttpClient, @Inject(API_ENDPOINT) private apiEndpoint) {}
  
  ...

  search(term: string) : Observable<Array<Contact>> {
  	const searchUrl = `${this.apiEndpoint}/search?text=${term}`;
	
    return this.http
		.get<ContactsResponse>(searchUrl)
        .pipe(map(data => data.items));
  }

}
```

###### `contacts-list.component.ts`

```ts
@Component({
  selector: 'trm-contacts-list',
  templateUrl: './contacts-list.component.html',
  styleUrls: ['./contacts-list.component.css']
})
export class ContactsListComponent implements OnInit {
  contacts$: Observable<Array<Contact>>;

  ...

  search(term: string) {
    this.contacts$ = this.contactsService.search(term);
  }
}
```

## Web and App Servers

To launch your web application and the REST server, use a Terminal session with the command:

```console
$   ./start
```



## Next Lab

Go to [Observables Lab #2: Debounce](exercise-2_debounce-distinctuntilchanged.md)
