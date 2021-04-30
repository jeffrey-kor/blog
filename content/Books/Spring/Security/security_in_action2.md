---
title: "Security_in_action2"
date: 2021-04-27T13:20:37+09:00
draft: true
categories:
  - "Category 1"
  - "Category 2"
tags:
  - "Test"
  - "Another test"
thumbnail: "img/placeholder.jpg"
comments: true
authorbox: true
pager: true
toc: true
sidebar: "right"
widgets:
  - "search"
  - "recent"
  - "taglist"
---
##### Spring Security

2. Security Context: 
1. Authentication Filter: The Request is intercepted by authentication filter 
2. Authentication Manager: Authentication responsibility is delegated to the authentication manager 
3. Authentication provider: The authentication manager uses the authentication provider, which implements the authentication logic
4. User Details service, password encoder: The authentication provider finds the user with a user details service and validates the password using a password encoder
5. From provider to manager: The result of authentication is returned to the filter
6. From Filter to Security Context: Details about the authenticated entitiy are stored in the security context

   
5. 
