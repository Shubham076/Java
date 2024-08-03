```java
package com.example.forwarder.controller;
import jakarta.servlet.http.HttpServletRequest;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.http.HttpEntity;
import org.springframework.http.HttpHeaders;
import org.springframework.http.HttpMethod;
import org.springframework.http.ResponseEntity;
import org.springframework.web.bind.annotation.*;
import org.springframework.web.client.RestTemplate;
import org.springframework.web.util.UriComponentsBuilder;
import java.net.URI;
import java.util.Enumeration;
import java.util.HashMap;
import java.util.Map;

@RestController
@RequestMapping("/api/v1")
public class Forwarder {


    private final RestTemplate restTemplate;

    @Autowired
    public Forwarder() {
        this.restTemplate = new RestTemplate();
    }

    public ResponseEntity<String> forwardRequest(
            String targetUrl,
            HttpMethod method,
            Map<String, String> headers,
            Map<String, String> queryParams,
            String body) {

        // Build the target URI with query parameters
        UriComponentsBuilder uriBuilder = UriComponentsBuilder.fromHttpUrl(targetUrl);
        queryParams.forEach(uriBuilder::queryParam);
        URI uri = uriBuilder.build().toUri();

        // Set headers
        HttpHeaders httpHeaders = new HttpHeaders();
        headers.forEach(httpHeaders::set);

        // Create the HTTP entity
        HttpEntity<String> entity = new HttpEntity<>(body, httpHeaders);

        // Forward the request
        return restTemplate.exchange(uri, method, entity, String.class);
    }

    @GetMapping("/**")
    public ResponseEntity<String> getHandler(HttpServletRequest request, HttpMethod method,
                             @RequestHeader Map<String, String> headers,
                             @RequestParam Map<String, String> queryParams,
                             @RequestBody String body) {
        String requestUri = request.getRequestURI();
        String queryString = request.getQueryString();
        System.out.println("Request URI: " + requestUri + ", Query String: " + queryString + ", Method: " + method);

        // Collect headers
        Map<String, String> headerMap = new HashMap<>();
        Enumeration<String> headerNames = request.getHeaderNames();
        while (headerNames.hasMoreElements()) {
            String headerName = headerNames.nextElement();
            headerMap.put(headerName, request.getHeader(headerName));
        }

        String targetUrl = "http://localhost:8000" +  requestUri;
        return forwardRequest(targetUrl, method, headers, queryParams, body);
    }

    @PostMapping("/**")
    public ResponseEntity<String> postHandler(HttpServletRequest request, HttpMethod method,
                                             @RequestHeader Map<String, String> headers,
                                             @RequestParam Map<String, String> queryParams,
                                             @RequestBody String body) {
        String requestUri = request.getRequestURI();
        String queryString = request.getQueryString();
        System.out.println("Request URI: " + requestUri + ", Query String: " + queryString + ", Method: " + method);

        // Collect headers
        Map<String, String> headerMap = new HashMap<>();
        Enumeration<String> headerNames = request.getHeaderNames();
        while (headerNames.hasMoreElements()) {
            String headerName = headerNames.nextElement();
            headerMap.put(headerName, request.getHeader(headerName));
        }

        String targetUrl = "http://localhost:8000" +  requestUri;
        return forwardRequest(targetUrl, method, headers, queryParams, body);
    }
}

```
