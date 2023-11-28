# HTTP

<p align="center"><img align="center" width="30%" height="30%" src="assets/http.svg"></p>

[Hypertext Transfer Protocol (HTTP)](https://en.wikipedia.org/wiki/HTTP) is an application layer protocol in the Internet protocol suite model for distributed, collaborative, hypermedia information systems that lay the foundation of data communication for the World Wide Web.

## Index

* [Methods](#methods)
* [REST](#rest)

## Methods

HTTP methods (`verbs`) indicate the desired action to be performed on the identified resource.

* `GET` method requests that the target resource transfer a representation of its state, it should only retrieve data and should have no other effect.
* `POST` method requests that the target resource process the representation enclosed in the request according to the semantics of the target resource.
* `PUT` method requests that the target resource create or update its state with the `total` state defined by the representation enclosed in the request.
* `PATCH` method requests that the target resource modify its state according to the `partial` update defined in the representation enclosed in the request.
* `DELETE` method requests that the target resource delete its state.

## REST

[Representational State Transfer (REST)](https://en.wikipedia.org/wiki/REST) is a software architectural style that was created to guide the design and development of the architecture for the World Wide Web.
It has been employed throughout the software industry to create [stateless](https://en.wikipedia.org/wiki/Stateless_protocol), [idempotent](https://en.wikipedia.org/wiki/Idempotence) and [reliable](https://en.wikipedia.org/wiki/Reliability,_availability_and_serviceability) Web-based applications and HTTP-based APIs.

* Use plural noums to represent collection of resources.
```
/customers/{id}
/customers/{id}/orders
/store/items/{id}
```

* Use hyphens instead of underscores.
```
/store/inventory-management
```

* Versioning.
```
/v1/customers/{id}
/v2/customers/{id}
```

* Filtering.
```
/customers?lastname=Smith&age=63
/customers?fields=id,age
```

* Sorting.
```
/customers?sort=lastname,age
```

* Pagination.
```
/customers?limit=50
/customers?start=0&limit=50
```
