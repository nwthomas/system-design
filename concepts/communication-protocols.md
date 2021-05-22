# COMMUNICATION PROTOCOLS

1. [Summary](#summary)
2. [AJAX Polling](#ajax-polling)
3. [HTTP Long-Polling](#http-long-polling)
4. [WebSockets](#websockets)
5. [Server-Sent Events (SSEs)](#server-sent-events-sses)

## SUMMARY

Long-Polling, WebSockets, and Server-Sent Events are popular communication protocols between a client like a web browser and a web server. First, let's start with understanding what a standard HTTP request is and what it looks like.

This is the sequence of events for a regular HTTP request:

1. The client opens a connection and requests data from the server
2. The server calculates the response
3. The server sends back the response to the client on the opened request

Example:

![Example HTTP request](../assets/example-http-request.png)

## AJAX POLLING

This is the technique used by most AJAX applications. The basic idea is that the client repeatedly polls (or requests) a server for data.

The problem with polling is that the client has to keep asking the server for any new data. As a result, a lot of responses are empty, creating HTTP overhead.

![AJAX Polling](../assets/ajax-polling.png)

## HTTP LONG-POLLING

This variation of the traditional polling described just above allows the server to push information to a client whenever the data is available. With Long-Polling, the client requests information from the server exactly as before but knows that the server might not respond immediately. This technique is also referred to as a "Hanging GET."

When a client finally gets a response from the server, it immediately requests again and allows the server to hold onto that requests indefinitely.

Each Long-Poll request will typically have a timeout. The client has to reconnect periodically after the connection is closed due to the timeout.

![HTTP Long-Polling](../assets/http-long-polling.png)

## WEBSOCKETS

## SERVER-SENT EVENTS (SSEs)
