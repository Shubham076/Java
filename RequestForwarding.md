```java
public ResponseEntity<String> forwardRequest(
            String targetUrl,
            HttpMethod method,
            @RequestHeader Map<String, String> headers,
            @RequestParam Map<String, String> queryParams,
            @PathVariable Map<String, String> pathParams,
            @RequestBody(required = false) String body) {

        // Build the target URI with query parameters
        UriComponentsBuilder uriBuilder = UriComponentsBuilder.fromHttpUrl(targetUrl);
        queryParams.forEach(uriBuilder::queryParam);
        URI uri = uriBuilder.buildAndExpand(pathParams).toUri();

        // Set headers
        HttpHeaders httpHeaders = new HttpHeaders();
        headers.forEach(httpHeaders::set);

        // Create the HTTP entity
        HttpEntity<String> entity = new HttpEntity<>(body, httpHeaders);

        // Forward the request
        return restTemplate.exchange(uri, method, entity, String.class);
    }
```
