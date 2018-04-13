---
title: API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - http

toc_footers:
  - <a href='#'>Sign Up for a Developer Key</a>
  - <a href='https://github.com/lord/slate'>Documentation Powered by Slate</a>

includes:
  - alerts
  - situations
  - errors

search: true
---

# Introduction

Welcome to the Graze API guide. You can use these API endpoints to integrate with external services and expose selected Moogsoft AIOps functionality to authorized external clients.

You can view code examples in the dark area to the right of the screen.

# Configuration

The Graze API is implemented as a set of servlets running in the Moogsoft AIOps Tomcat instance that handles external Graze requests, making the UI servlet calls directly via cross-contexts. 

Tomcat must be configured to allow cross-context calls to be made by adding the following to the context.xml file in the Tomcat $APPSERVER_HOME/conf directory:
```http
<Context crossContext="true">
```

# Authentication

The Graze API supports basic authentication. You can use the default Grazer user credentials for this:

```http
username: graze
password: graze
```

All Graze requests use the following URL format, where `<server>` is the hostname of your AIOps instance:

```http
https://<server>/graze/v1/authenticate
```
All requests, other than `authenticate` require a basic authentication header or a valid `auth_token`. A valid `authenticate` request must be made before you can send a Graze request without a basic authentication header.

Inactive sessions are logged out after an hour and a new `authenticate` request must be sent to get a new `auth_token`.
<aside class="notice">
If you are making regular Graze endpoints within an hour timeframe, you are considered active and your session will not expire.
</aside>
