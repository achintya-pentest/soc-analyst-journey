# Web Server Log Investigation

## Scenario

During web server monitoring, unusual HTTP requests were observed in the server access logs. The goal of this investigation was to analyze the HTTP requests and determine whether the activity was normal browsing behavior or potential reconnaissance activity.

## Sample Log Entries

```
192.168.1.5 - - "GET /admin HTTP/1.1" 404
192.168.1.5 - - "GET /admin.php HTTP/1.1" 404
192.168.1.5 - - "GET /login HTTP/1.1" 200
192.168.1.5 - - "GET /phpmyadmin HTTP/1.1" 404
```

## Log Breakdown

* **192.168.1.5** → Client IP address making the request
* **GET** → HTTP request method
* **Requested resource** → The page being accessed
* **HTTP/1.1** → HTTP protocol version
* **Status code** → Server response

## Analysis

The same IP address attempted to access multiple sensitive directories such as `/admin` and `/phpmyadmin`. Most requests resulted in **404 (Not Found)** responses.

This pattern may indicate automated scanning for common administrative panels or vulnerable endpoints.

## Findings

The repeated access attempts to administrative paths suggest possible **directory enumeration or reconnaissance activity**.

## Conclusion

Web server logs can reveal suspicious activity such as directory scanning or attempts to discover sensitive resources. Monitoring HTTP requests and status codes helps SOC analysts detect early reconnaissance attempts against web applications.
