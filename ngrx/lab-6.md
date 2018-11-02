# NgRx Lab 6: Use NgRx Facade


### Scenario

NgRx **Facades** provide a public API layer between the NgRx layers and the View component layers. 

Architectures with Facades allow developers to implement views that maintain 1-way data flows and passively render *pushed data*.


### Code Instructions

Let's implement a TicketsFacade that encapsulates all the selectors to build Store Queries (e.g. `this.store.pipe(select(ticketsQuery.getAllTickets))`) and all store action dispatching.

  > Store queries are observables to specific NgRx state data; extracted with memoized selectors.

<br/>

----
  

##### In `libs/tickets-state/src/lib/+state/tickets.facade.ts`

1. Inject the Store using `private readonly store: Store<PartialAppState>`
2. Implement the following Query Observables using `store.pipe(select(<query>))`:
  * `allItems$`
  * `entities$`
  * `isLoading$`
  * `error$`  
3. Implement a `loadTicketById(ticketId)` public method that dispatches a LoadTicket action.

> Be sure to register the Facade as a service within the `tickets-state.module.ts`! And don't forget to add this service to the library barrel/Public API.

##### In `ticket-details.component.ts`

1. Replace the deprecated injection of Store within an injected Facade instance using `private facade: TicketsFacade`
2. Replace all uses of `store.pipe(select(<query>)` with `facade.entities$.pipe(...)`
3. Remove the dispatching of the `LoadTicket` action

##### In `ticket-list.component.ts`

1. Replace the deprecated injection of Store within an injected Facade instance using `private facade: TicketsFacade`
2. Replace all uses of `store.pipe(select(<query>)` with `facade.allItems$.pipe(...)`
3. Remove the dispatching of the `LoadTicket` action

<br/>

### Code Snippets

###### `tickets.facade.ts`
![tickets.facade.ts](https://user-images.githubusercontent.com/210413/47938099-fc1a6a00-deb0-11e8-94f7-efd294104052.png)

###### `ticket-details.component.ts`
![ticket-details.component.ts](https://user-images.githubusercontent.com/210413/47938113-03da0e80-deb1-11e8-8094-acf9e9c39be6.png)

###### `ticket-list.component.ts`
![ticket-list.component.ts](https://user-images.githubusercontent.com/210413/47938126-0c324980-deb1-11e8-9b3c-94a78482dc73.png)

###### `tickets-state.module.ts`
![tickets-state.module.ts](https://user-images.githubusercontent.com/210413/47938212-574c5c80-deb1-11e8-9306-1159e67492ba.png)

<br/>

----

<br/>

### Investigate

Why is the TicketDetails using the `entities$` query instead of the `allItems$`?

Be prepared to discuss this? 

<br/>

### Running the Application

*  Open the **Customer Portal** application with the browser: http://localhost:4203
*  Confirm the **Node Server** is running with browser page:  http://localhost:3000/api/tickets

Run the following command(s) in individual terminals:

```console
yarn server
```

```console
yarn customer-portal -- -o
```

> If you already have one(s) running and need to restart, you can stop the run with `ctrl+c`.


<br/>

----

<br/>

## Next Lab

Go to NgRx Lab #7: [Use NgRx Facade](lab-6.md)