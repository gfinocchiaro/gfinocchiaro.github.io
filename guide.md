<div id="header">

Getting Started Guide
=====================

<div class="details">

[The Lightstreamer Team]{#author .author}\
[<support@lightstreamer.com>]{#email .email}\
[version 1.1,]{#revnumber} [September 29, 2017]{#revdate}

</div>

<div id="toc" class="toc2">

<div id="toctitle">

Table of Contents

</div>

-   [1. Introduction](#_introduction)
    -   [1.1. What Is MQTT.Cool?](#_what_is_mqtt_cool)
        -   [1.1.1. Architecture Extensions](#_architecture_extensions)
        -   [1.1.2. Performance Extensions](#_performance_extensions)
        -   [1.1.3. Security Extensions](#_security_extensions)
    -   [1.2. MQTT.Cool Architecture](#_mqtt_cool_architecture)
    -   [1.3. Quick Start](#_quick_start)
        -   [1.3.1. Check System
            Requirements](#_check_system_requirements)
        -   [1.3.2. Download and Install](#_download_and_install)
        -   [1.3.3. Configure](#_configure)
        -   [1.3.4. Attach an MQTT Broker](#_attach_an_mqtt_broker)
        -   [1.3.5. Start](#_start)
        -   [1.3.6. Check](#_check)
    -   [1.4. Hello IoT World Tutorial](#_hello_iot_world_tutorial)
        -   [1.4.1. Step 1: Setup an MQTT
            Broker](#_step_1_setup_an_mqtt_broker)
        -   [1.4.2. Step 2: Attach the MQTT
            Broker](#_step_2_attach_the_mqtt_broker)
        -   [1.4.3. Step 3: Write the Feed
            Simulator](#_step_3_write_the_feed_simulator)
        -   [1.4.4. Step 4: Make the JavaScript
            Client](#_step_4_make_the_javascript_client)
-   [2. Addressing MQTT Brokers](#_addressing_mqtt_brokers)
    -   [2.1. Static Lookup](#static_lookup)
        -   [2.1.1. The Hook Variant](#static_lookup_hook)
        -   [2.1.2. Client Side Settings](#_client_side_settings)
        -   [2.1.3. Final Considerations](#_final_considerations)
    -   [2.2. Dynamic Lookup](#dynamic_lookup)
        -   [2.2.1. Client Side Settings](#_client_side_settings_2)
        -   [2.2.2. Final Considerations](#_final_considerations_2)
-   [3. Client Application
    Development](#_client_application_development)
    -   [3.1. The SDKs](#_the_sdks)
        -   [3.1.1. Deployment Architecture](#_deployment_architecture)
    -   [3.2. SDK for Web Clients](#_sdk_for_web_clients)
        -   [3.2.1. Installation](#_installation)
        -   [3.2.2. The UMD Pattern](#_the_umd_pattern)
        -   [3.2.3. CommonJS](#_commonjs)
    -   [3.3. SDK for Node.js Clients](#_sdk_for_node_js_clients)
    -   [3.4. The MQTT.Cool Connection Pattern](#connection_pattern)
    -   [3.5. The MQTTCoolSession Interface](#session_interface)
    -   [3.6. The MqttClient Interface](#_the_mqttclient_interface)
        -   [3.6.1. Multiplexed MQTT
            Channels](#_multiplexed_mqtt_channels)
        -   [3.6.2. Dedicated End-to-End
            Connection](#dedicated_connection)
        -   [3.6.3. Shared End-to-End Connection](#shared_connection)
    -   [3.7. Specifying Connection Options](#connection_options)
        -   [3.7.1. Managing Persistent
            Session](#_managing_persistent_session)
        -   [3.7.2. Managing Connection Lost](#managing_connection_lost)
    -   [3.8. The Message Class](#_the_message_class)
    -   [3.9. Publishing](#_publishing)
        -   [3.9.1. Message Delivery
            Notification](#message_delivery_notifications)
    -   [3.10. Subscribing](#_subscribing)
        -   [3.10.1. Topic Filter](#_topic_filter)
        -   [3.10.2. Subscribe Options](#subscribe_options)
        -   [3.10.3. Message Arriving
            Notification](#_message_arriving_notification)
    -   [3.11. Unsubscribing](#unsubscribing)
    -   [3.12. Reconnecting](#reconnecting)
        -   [3.12.1. The MqttClient Session
            State](#_the_mqttclient_session_state)
        -   [3.12.2. Starting to Reconnect](#starting_to_reconnect)
        -   [3.12.3. Completing Reconnection](#_completing_reconnection)
    -   [3.13. Disconnecting](#disconnecting)
-   [4. The MQTT.Cool Hook](#_the_mqtt_cool_hook)
    -   [4.1. Basics](#_basics)
    -   [4.2. Hook Development](#_hook_development)
        -   [4.2.1. Setting Up the Development
            Environment](#_setting_up_the_development_environment)
        -   [4.2.2. The MQTTCoolHook
            Interface](#_the_mqttcoolhook_interface)
        -   [4.2.3. Notifying of Hook
            Initialization](#_notifying_of_hook_initialization)
        -   [4.2.4. Authorizing Session
            Opening](#hook_authorizing_session)
        -   [4.2.5. Authorizing
            Connection](#hook_authorizing_connection)
        -   [4.2.6. Authorizing Message
            Publishing](#hook_authorizing_publishing)
        -   [4.2.7. Authorizing
            Subscription](#hook_authorizing_subscription)
        -   [4.2.8. Notifying of Session Closing, Disconnection and
            Unsubscription](#_notifying_of_session_closing_disconnection_and_unsubscription)
    -   [4.3. Packaging, Configuration and
        Deployment](#_packaging_configuration_and_deployment)
-   [Appendix A: Connection Parameters](#_connection_parameters)
-   [Appendix B: Access the Lightstreamer Client
    API](#_access_the_lightstreamer_client_api)
    -   [B.1. The LightstreamerClient
        Object](#_the_lightstreamerclient_object)
        -   [B.1.1. Managing the Connection
            Options](#_managing_the_connection_options)
    -   [B.2. Bandwidth Throttling](#_bandwidth_throttling)
    -   [B.3. Attaching a Listener](#_attaching_a_listener)
    -   [B.4. Private Operations](#_private_operations)

</div>

</div>

<div id="content">

<div class="sect1">

1. Introduction {#_introduction}
---------------

<div class="sectionbody">

<div class="sect2">

### 1.1. What Is MQTT.Cool? {#_what_is_mqtt_cool}

<div class="paragraph">

MQTT.Cool is a gateway designed for boosting existing MQTT brokers by
extending their native functionalities with new out-of-the-box features.

</div>

<div class="paragraph">

MQTT.Cool provides architecture extensions, performance extensions, and
security extensions to any third-party MQTT broker, as detailed below.

</div>

<div class="sect3">

#### 1.1.1. Architecture Extensions {#_architecture_extensions}

<div class="sect4">

##### Connect to Any MQTT Broker from Anywhere {#_connect_to_any_mqtt_broker_from_anywhere}

<div class="paragraph">

Connect to your MQTT broker from anywhere on the Internet, even behind
the strictest corporate firewalls and proxies, without sacrificing
security. No need to fight with firewall rules and change your security
policies.

</div>

<div class="paragraph">

Your MQTT broker will be instantly available through standard Web
protocols (HTTP and WebSockets). This means your MQTT broker does not
need to support WebSockets, because it’s up to MQTT.Cool to re-encode
the MQTT protocol into a very efficient and firewall-friendly protocol
(called the *Lightstreamer protocol*).

</div>

<div class="paragraph">

Even if WebSockets are not supported by the network infrastructure (for
instance, they might be blocked by a client-side proxy), the connection
will automatically work over HTTP, thanks to StreamSense,
Lightstreamer’s state-of-the-art implementation of HTTP streaming and
HTTP long polling.

</div>

<div class="paragraph">

What happens if a client gets disconnected, for any reason? No worries,
the MQTT.Cool client library will automatically reconnect and
re-establish the correct subscriptions.

</div>

</div>

<div class="sect4">

##### Develop Web Clients with Our Eclipse Paho-like API {#_develop_web_clients_with_our_eclipse_paho_like_api}

<div class="paragraph">

We provide you with a JavaScript library that works in any existing
browser, including mobile browsers, as well as Node.js.

</div>

<div class="paragraph">

The library exposes an Eclipse Paho-like API. Any HTML page can easily
become an MQTT client, able to publish and subscribe to/from MQTT
topics, irrespective of which MQTT broker you are using. This way, web
pages can exchange messages with IoT devices and existing MQTT
applications, as well as interact with other web pages in real time.

</div>

<div class="paragraph">

Similarly, any Node.js application will be able to access any MQTT
broker and produce/consume messages.

</div>

</div>

<div class="sect4">

##### Access Multiple MQTT Brokers {#_access_multiple_mqtt_brokers}

<div class="paragraph">

A single MQTT.Cool instance can connect to different MQTT brokers. For
example, it might connect to both a Mosquitto instance and a HiveMQ
instance and make these brokers available to the clients. If the same
client needs to access both the brokers, it will be able to do it with a
single physical connection to MQTT.Cool, because all the traffic is
multiplexed over a single link for each client.

</div>

</div>

</div>

<div class="sect3">

#### 1.1.2. Performance Extensions {#_performance_extensions}

<div class="sect4">

##### Scale Up Your MQTT Broker with Massive Fan-Out {#_scale_up_your_mqtt_broker_with_massive_fan_out}

<div class="paragraph">

Scale to millions of MQTT clients by offloading the fan-out from your
existing MQTT broker to MQTT.Cool.

</div>

<div class="paragraph">

Clients will physically connect to MQTT.Cool, which uses the world-class
Lightstreamer engine to handle massively concurrent connections.
MQTT.Cool scales horizontally by automatically employing all the
available cores; and it scales vertically with multiple instances
managed by any common load balancer.

</div>

</div>

<div class="sect4">

##### Always Receive Fresh Data with Adaptive Throttling and Conflation {#_always_receive_fresh_data_with_adaptive_throttling_and_conflation}

<div class="paragraph">

Imagine an IoT sensor that produces hundreds of measurements per second
and publishes them on MQTT. You have a web page showing such data in
real time.

</div>

<div class="paragraph">

Now, imagine a user watching that page on a desktop browser with a
broadband connection and another user watching the same page on a mobile
browser with a bad signal. MQTT.Cool will automatically throttle the
data flow for each user, to adapt to any network congestion. It will
resample the data on the fly, while applying conflation, so that the two
users will both see real-time and coherent data, but with different
update rates.

</div>

</div>

<div class="sect4">

##### Get Full Control over Bandwidth and Frequency {#_get_full_control_over_bandwidth_and_frequency}

<div class="paragraph">

In addition to adaptive throttling, each client can explicitly configure
a maximum bandwidth for its downstream channel. For example, a client
might request to never consume more than 10 kbps. Queuing, resampling,
and conflation will be applied automatically to respect the allocated
bandwidth.

</div>

<div class="paragraph">

Similarly, a maximum update frequency can be requested by each client
for every shared subscription. For example, a client might subscribe to
a topic specifying that no more than 2 messages per second must be
delivered.

</div>

</div>

</div>

<div class="sect3">

#### 1.1.3. Security Extensions {#_security_extensions}

<div class="sect4">

##### Authenticate Users with Total Flexibility {#_authenticate_users_with_total_flexibility}

<div class="paragraph">

Typical MQTT authentication is based on username and password only.
Furthermore, it can be a nightmare to integrate MQTT authentication
offered by a typical MQTT broker with existing enterprise authentication
systems.

</div>

<div class="paragraph">

MQTT.Cool offers a pluggable authentication system, which is totally
independent of the target MQTT broker. Users' authentication is managed
by MQTT.Cool via your own integration code, based on the *Hook API*. Not
only will your authentication code be able to receive a username and
password, but it will be passed full context information, including
client remote IP, user agent, cookies, client-side certificates, etc.

</div>

<div class="paragraph">

It is straightforward to develop a Hook that integrates MQTT.Cool with
an existing user DB. And you can switch MQTT broker without losing your
authentication logic.

</div>

</div>

<div class="sect4">

##### Add Fine-Grained Authorization {#_add_fine_grained_authorization}

<div class="paragraph">

How do you make sure that user A cannot subscribe to topic X and user B
cannot publish to topic Y? This is left to each MQTT broker proprietary
authorization system (if available at all).

</div>

<div class="paragraph">

With MQTT.Cool, you can add very fine-grained authorization to any MQTT
broker, in a completely broker-agnostic way. With the Hook API, any
action performed by a user is authorized via a specific callback to your
own code. As for authentication, you have total flexibility in defining
your security policies, based on your very needs. And, again, you can
switch MQTT broker without losing your authorization logic.

</div>

</div>

<div class="sect4">

##### Offload TLS/SSL Encryption {#_offload_tls_ssl_encryption}

<div class="paragraph">

MQTT.Cool can take care of encrypting the traffic with the clients,
based on TLS/SSL configurable cipher suites and certificates. This way,
you can remove the burden of encryption from your MQTT broker and
offload it to MQTT.Cool, which uses WSS and HTTPS for the client
connections.

</div>

</div>

<div class="sect4">

##### Increase Security by Avoiding Public Access to the Broker {#_increase_security_by_avoiding_public_access_to_the_broker}

<div class="paragraph">

You might want to hide or firewall-protect the connection details of
your MQTT broker (address and port) and make it reachable from the
Internet only through MQTT.Cool, which will reside in the DMZ. This way,
you will add a layer of security, preventing the broker from dealing
with external and potentially unauthorized connections.

</div>

</div>

</div>

</div>

<div class="sect2">

### 1.2. MQTT.Cool Architecture {#_mqtt_cool_architecture}

<div class="paragraph">

MQTT.Cool is a stand-alone server, which can be installed on any
machine, be it physical or virtual, either in the cloud or on premises.

</div>

<div class="paragraph">

MQTT.Cool connects to any existing MQTT broker and acts as a
**gateway**. Clients use the provided MQTT.Cool APIs, which are Eclipse
Paho-like, to connect to the MQTT.Cool server.

</div>

<div id="deployment" class="imageblock" style="text-align: center">

<div class="content">

![architecture](data:image/svg+xml;base64,PCFET0NUWVBFIHN2ZyBQVUJMSUMgIi0vL1czQy8vRFREIFNWRyAxLjEvL0VOIiAiaHR0cDovL3d3dy53My5vcmcvR3JhcGhpY3MvU1ZHLzEuMS9EVEQvc3ZnMTEuZHRkIj4KPHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHhtbG5zOnhsaW5rPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hsaW5rIiB3aWR0aD0iOTkxcHgiIGhlaWdodD0iMzQxcHgiIHZlcnNpb249IjEuMSIgc3R5bGU9ImJhY2tncm91bmQtY29sb3I6IHJnYigyNTUsIDI1NSwgMjU1KTsiPjxkZWZzLz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgwLjUsMC41KSI+PHJlY3QgeD0iMCIgeT0iMCIgd2lkdGg9Ijk5MCIgaGVpZ2h0PSIzNDAiIGZpbGw9IiNmZmZmZmYiIHN0cm9rZT0ibm9uZSIgcG9pbnRlci1ldmVudHM9Im5vbmUiLz48cGF0aCBkPSJNIDI2NiAxMzMgQyAyMzQuOCAxMzMgMjI3IDE3MiAyNTEuOTYgMTc5LjggQyAyMjcgMTk2Ljk2IDI1NS4wOCAyMzQuNCAyNzUuMzYgMjE4LjggQyAyODkuNCAyNTAgMzM2LjIgMjUwIDM1MS44IDIxOC44IEMgMzgzIDIxOC44IDM4MyAxODcuNiAzNjMuNSAxNzIgQyAzODMgMTQwLjggMzUxLjggMTA5LjYgMzI0LjUgMTI1LjIgQyAzMDUgMTAxLjggMjczLjggMTAxLjggMjY2IDEzMyBaIiBmaWxsPSIjZmZmZmZmIiBzdHJva2U9IiMyYTVlNzQiIHN0cm9rZS13aWR0aD0iMiIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0ibm9uZSIvPjxnIGZpbGw9IiMyQTVFNzQiIGZvbnQtZmFtaWx5PSJIZWx2ZXRpY2EiIHRleHQtYW5jaG9yPSJtaWRkbGUiIGZvbnQtc2l6ZT0iMThweCI+PHRleHQgeD0iMzA0IiB5PSIxNzgiPkludGVybmV0PC90ZXh0PjwvZz48cmVjdCB4PSI3NjkiIHk9IjEyOSIgd2lkdGg9IjEwMCIgaGVpZ2h0PSI4MCIgcng9IjEyIiByeT0iMTIiIGZpbGw9IiNjMDc1MWYiIHN0cm9rZT0ibm9uZSIgcG9pbnRlci1ldmVudHM9Im5vbmUiLz48ZyBmaWxsPSIjRkZGRkZGIiBmb250LWZhbWlseT0iSGVsdmV0aWNhIiB0ZXh0LWFuY2hvcj0ibWlkZGxlIiBmb250LXNpemU9IjE0cHgiPjx0ZXh0IHg9IjgxOC41IiB5PSIxNzMuNSI+TVFUVCBCcm9rZXI8L3RleHQ+PC9nPjxwYXRoIGQ9Ik0gNjg5LjI0IDE2OCBMIDc1My43NiAxNjgiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzJhNWU3NCIgc3Ryb2tlLXdpZHRoPSIyIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJub25lIi8+PHBhdGggZD0iTSA2ODEuMjQgMTY4IEwgNjg5LjI0IDE2NCBMIDY4OS4yNCAxNzIgWiIgZmlsbD0iIzJhNWU3NCIgc3Ryb2tlPSIjMmE1ZTc0IiBzdHJva2Utd2lkdGg9IjIiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9Im5vbmUiLz48cGF0aCBkPSJNIDc2MS43NiAxNjggTCA3NTMuNzYgMTcyIEwgNzUzLjc2IDE2NCBaIiBmaWxsPSIjMmE1ZTc0IiBzdHJva2U9IiMyYTVlNzQiIHN0cm9rZS13aWR0aD0iMiIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0ibm9uZSIvPjxnIGZpbGw9IiMyQTVFNzQiIGZvbnQtZmFtaWx5PSJIZWx2ZXRpY2EiIGZvbnQtd2VpZ2h0PSJib2xkIiB0ZXh0LWFuY2hvcj0ibWlkZGxlIiBmb250LXNpemU9IjEycHgiPjxyZWN0IGZpbGw9IiNmZmZmZmYiIHN0cm9rZT0ibm9uZSIgeD0iNzEyIiB5PSIxNDMiIHdpZHRoPSIzNiIgaGVpZ2h0PSIxNSIgc3Ryb2tlLXdpZHRoPSIwIi8+PHRleHQgeD0iNzI5IiB5PSIxNTMiPk1RVFQ8L3RleHQ+PC9nPjxwYXRoIGQ9Ik0gMzg5LjI0IDE2OCBMIDQ0OC43NiAxNjgiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzJhNWU3NCIgc3Ryb2tlLXdpZHRoPSIyIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJub25lIi8+PHBhdGggZD0iTSAzODEuMjQgMTY4IEwgMzg5LjI0IDE2NCBMIDM4OS4yNCAxNzIgWiIgZmlsbD0iIzJhNWU3NCIgc3Ryb2tlPSIjMmE1ZTc0IiBzdHJva2Utd2lkdGg9IjIiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9Im5vbmUiLz48cGF0aCBkPSJNIDQ1Ni43NiAxNjggTCA0NDguNzYgMTcyIEwgNDQ4Ljc2IDE2NCBaIiBmaWxsPSIjMmE1ZTc0IiBzdHJva2U9IiMyYTVlNzQiIHN0cm9rZS13aWR0aD0iMiIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0ibm9uZSIvPjxnIGZpbGw9IiMyQTVFNzQiIGZvbnQtZmFtaWx5PSJIZWx2ZXRpY2EiIGZvbnQtd2VpZ2h0PSJib2xkIiB0ZXh0LWFuY2hvcj0ibWlkZGxlIiBmb250LXNpemU9IjEycHgiPjxyZWN0IGZpbGw9IiNmZmZmZmYiIHN0cm9rZT0ibm9uZSIgeD0iMzkyIiB5PSIxNDMiIHdpZHRoPSI1NiIgaGVpZ2h0PSIxNSIgc3Ryb2tlLXdpZHRoPSIwIi8+PHRleHQgeD0iNDE5IiB5PSIxNTMiPldTL0hUVFA8L3RleHQ+PC9nPjxyZWN0IHg9IjcxNCIgeT0iMjU5IiB3aWR0aD0iODAiIGhlaWdodD0iNDAiIGZpbGw9IiM3NDUyMmEiIHN0cm9rZT0ibm9uZSIgcG9pbnRlci1ldmVudHM9Im5vbmUiLz48ZyBmaWxsPSIjRkZGRkZGIiBmb250LWZhbWlseT0iSGVsdmV0aWNhIiB0ZXh0LWFuY2hvcj0ibWlkZGxlIiBmb250LXNpemU9IjEycHgiPjx0ZXh0IHg9Ijc1My41IiB5PSIyODIuNSI+TVFUVCBDbGllbnQ8L3RleHQ+PC9nPjxyZWN0IHg9IjcxNCIgeT0iMjkiIHdpZHRoPSI4MCIgaGVpZ2h0PSI0MCIgZmlsbD0iIzc0NTIyYSIgc3Ryb2tlPSJub25lIiBwb2ludGVyLWV2ZW50cz0ibm9uZSIvPjxnIGZpbGw9IiNGRkZGRkYiIGZvbnQtZmFtaWx5PSJIZWx2ZXRpY2EiIHRleHQtYW5jaG9yPSJtaWRkbGUiIGZvbnQtc2l6ZT0iMTJweCI+PHRleHQgeD0iNzUzLjUiIHk9IjUyLjUiPk1RVFQgQ2xpZW50PC90ZXh0PjwvZz48cmVjdCB4PSI4NDQiIHk9IjI1OSIgd2lkdGg9IjgwIiBoZWlnaHQ9IjQwIiBmaWxsPSIjNzQ1MjJhIiBzdHJva2U9Im5vbmUiIHBvaW50ZXItZXZlbnRzPSJub25lIi8+PGcgZmlsbD0iI0ZGRkZGRiIgZm9udC1mYW1pbHk9IkhlbHZldGljYSIgdGV4dC1hbmNob3I9Im1pZGRsZSIgZm9udC1zaXplPSIxMnB4Ij48dGV4dCB4PSI4ODMuNSIgeT0iMjgyLjUiPk1RVFQgQ2xpZW50PC90ZXh0PjwvZz48cmVjdCB4PSI4NDQiIHk9IjI5IiB3aWR0aD0iODAiIGhlaWdodD0iNDAiIGZpbGw9IiM3NDUyMmEiIHN0cm9rZT0ibm9uZSIgcG9pbnRlci1ldmVudHM9Im5vbmUiLz48ZyBmaWxsPSIjRkZGRkZGIiBmb250LWZhbWlseT0iSGVsdmV0aWNhIiB0ZXh0LWFuY2hvcj0ibWlkZGxlIiBmb250LXNpemU9IjEycHgiPjx0ZXh0IHg9Ijg4My41IiB5PSI1Mi41Ij5NUVRUIENsaWVudDwvdGV4dD48L2c+PHBhdGggZD0iTSA3ODkuNSAxMjIuMjUgTCA3NTguNSA3NS43NSIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjYzA3NTFmIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJub25lIi8+PHBhdGggZD0iTSA3OTMuMzggMTI4LjA3IEwgNzg2LjU4IDEyNC4xOSBMIDc5Mi40MSAxMjAuMyBaIiBmaWxsPSIjYzA3NTFmIiBzdHJva2U9IiNjMDc1MWYiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9Im5vbmUiLz48cGF0aCBkPSJNIDc1NC42MiA2OS45MyBMIDc2MS40MiA3My44MSBMIDc1NS41OSA3Ny43IFoiIGZpbGw9IiNjMDc1MWYiIHN0cm9rZT0iI2MwNzUxZiIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0ibm9uZSIvPjxwYXRoIGQ9Ik0gODQ4LjUgMTIyLjI1IEwgODc5LjUgNzUuNzUiIGZpbGw9Im5vbmUiIHN0cm9rZT0iI2MwNzUxZiIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0ibm9uZSIvPjxwYXRoIGQ9Ik0gODQ0LjYyIDEyOC4wNyBMIDg0NS41OSAxMjAuMyBMIDg1MS40MiAxMjQuMTkgWiIgZmlsbD0iI2MwNzUxZiIgc3Ryb2tlPSIjYzA3NTFmIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJub25lIi8+PHBhdGggZD0iTSA4ODMuMzggNjkuOTMgTCA4ODIuNDEgNzcuNyBMIDg3Ni41OCA3My44MSBaIiBmaWxsPSIjYzA3NTFmIiBzdHJva2U9IiNjMDc1MWYiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9Im5vbmUiLz48cGF0aCBkPSJNIDg0OS4wNyAyMTUuMzQgTCA4NzguOTMgMjUyLjY2IiBmaWxsPSJub25lIiBzdHJva2U9IiNjMDc1MWYiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9Im5vbmUiLz48cGF0aCBkPSJNIDg0NC43IDIwOS44NyBMIDg1MS44IDIxMy4xNSBMIDg0Ni4zNCAyMTcuNTMgWiIgZmlsbD0iI2MwNzUxZiIgc3Ryb2tlPSIjYzA3NTFmIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJub25lIi8+PHBhdGggZD0iTSA4ODMuMyAyNTguMTMgTCA4NzYuMiAyNTQuODUgTCA4ODEuNjYgMjUwLjQ3IFoiIGZpbGw9IiNjMDc1MWYiIHN0cm9rZT0iI2MwNzUxZiIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0ibm9uZSIvPjxwYXRoIGQ9Ik0gNzU5LjA3IDI1Mi42NiBMIDc4OC45MyAyMTUuMzQiIGZpbGw9Im5vbmUiIHN0cm9rZT0iI2MwNzUxZiIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0ibm9uZSIvPjxwYXRoIGQ9Ik0gNzU0LjcgMjU4LjEzIEwgNzU2LjM0IDI1MC40NyBMIDc2MS44IDI1NC44NSBaIiBmaWxsPSIjYzA3NTFmIiBzdHJva2U9IiNjMDc1MWYiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9Im5vbmUiLz48cGF0aCBkPSJNIDc5My4zIDIwOS44NyBMIDc5MS42NiAyMTcuNTMgTCA3ODYuMiAyMTMuMTUgWiIgZmlsbD0iI2MwNzUxZiIgc3Ryb2tlPSIjYzA3NTFmIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJub25lIi8+PHBhdGggZD0iTSAxOTAuNDggMTEyLjI1IEwgMjMzLjUyIDEzNy43NSIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMmE1ZTc0IiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJub25lIi8+PHBhdGggZD0iTSAxODUuOTYgMTA5LjU3IEwgMTkzLjc3IDExMC4xMyBMIDE5MC40OCAxMTIuMjUgTCAxOTAuMiAxMTYuMTUgWiIgZmlsbD0iIzJhNWU3NCIgc3Ryb2tlPSIjMmE1ZTc0IiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJub25lIi8+PHBhdGggZD0iTSAyMzguMDQgMTQwLjQzIEwgMjMwLjIzIDEzOS44NyBMIDIzMy41MiAxMzcuNzUgTCAyMzMuOCAxMzMuODUgWiIgZmlsbD0iIzJhNWU3NCIgc3Ryb2tlPSIjMmE1ZTc0IiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJub25lIi8+PHJlY3QgeD0iNDY3IiB5PSI2NCIgd2lkdGg9IjIwNyIgaGVpZ2h0PSIyMTAiIHJ4PSIzMS4wNSIgcnk9IjMxLjA1IiBmaWxsPSIjMmE1ZTc0IiBzdHJva2U9Im5vbmUiIHBvaW50ZXItZXZlbnRzPSJub25lIi8+PGcgZmlsbD0iI0ZGRkZGRiIgZm9udC1mYW1pbHk9IkhlbHZldGljYSIgdGV4dC1hbmNob3I9Im1pZGRsZSIgZm9udC1zaXplPSIxN3B4Ij48dGV4dCB4PSI1NzAiIHk9IjI2Ny41Ij5NUVRULkNvb2w8L3RleHQ+PC9nPjxyZWN0IHg9IjQ3NyIgeT0iMjExIiB3aWR0aD0iMTg3IiBoZWlnaHQ9IjM1IiByeD0iNS4yNSIgcnk9IjUuMjUiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzMyOTZjMCIgc3Ryb2tlLXdpZHRoPSIyIiBwb2ludGVyLWV2ZW50cz0ibm9uZSIvPjxnIGZpbGw9IiNGRkZGRkYiIGZvbnQtZmFtaWx5PSJIZWx2ZXRpY2EiIHRleHQtYW5jaG9yPSJtaWRkbGUiIGZvbnQtc2l6ZT0iMTRweCI+PHRleHQgeD0iNTY5LjUiIHk9IjIzMi41Ij5MaWdodHN0cmVhbWVyIEVuZ2luZTwvdGV4dD48L2c+PHJlY3QgeD0iNDMiIHk9Ijg5IiB3aWR0aD0iMTQyIiBoZWlnaHQ9IjQwIiBmaWxsPSIjNTlhMmMwIiBzdHJva2U9Im5vbmUiIHBvaW50ZXItZXZlbnRzPSJub25lIi8+PGcgZmlsbD0iI0ZGRkZGRiIgZm9udC1mYW1pbHk9IkhlbHZldGljYSIgdGV4dC1hbmNob3I9Im1pZGRsZSIgZm9udC1zaXplPSIxNHB4Ij48dGV4dCB4PSIxMTMuNSIgeT0iMTEzLjUiPk1RVFQuQ29vbCBBUEk8L3RleHQ+PC9nPjxyZWN0IHg9IjQzIiB5PSIyOSIgd2lkdGg9IjE0MiIgaGVpZ2h0PSI2MCIgZmlsbD0iIzMyOTZjMCIgc3Ryb2tlPSJub25lIiBwb2ludGVyLWV2ZW50cz0ibm9uZSIvPjxnIGZpbGw9IiNGRkZGRkYiIGZvbnQtZmFtaWx5PSJIZWx2ZXRpY2EiIHRleHQtYW5jaG9yPSJtaWRkbGUiIGZvbnQtc2l6ZT0iMTRweCI+PHRleHQgeD0iMTEzLjUiIHk9IjYzLjUiPldlYiBCcm93c2VyIENsaWVudDwvdGV4dD48L2c+PHJlY3QgeD0iNDMiIHk9IjIwMiIgd2lkdGg9IjE0MiIgaGVpZ2h0PSI1MCIgZmlsbD0iIzMyOTZjMCIgc3Ryb2tlPSJub25lIiBwb2ludGVyLWV2ZW50cz0ibm9uZSIvPjxnIGZpbGw9IiNGRkZGRkYiIGZvbnQtZmFtaWx5PSJIZWx2ZXRpY2EiIHRleHQtYW5jaG9yPSJtaWRkbGUiIGZvbnQtc2l6ZT0iMTRweCI+PHRleHQgeD0iMTEzLjUiIHk9IjIzMS41Ij5Ob2RlLmpzIENsaWVudDwvdGV4dD48L2c+PHJlY3QgeD0iNDMiIHk9IjI1MiIgd2lkdGg9IjE0MiIgaGVpZ2h0PSI0MCIgZmlsbD0iIzU5YTJjMCIgc3Ryb2tlPSJub25lIiBwb2ludGVyLWV2ZW50cz0ibm9uZSIvPjxnIGZpbGw9IiNGRkZGRkYiIGZvbnQtZmFtaWx5PSJIZWx2ZXRpY2EiIHRleHQtYW5jaG9yPSJtaWRkbGUiIGZvbnQtc2l6ZT0iMTRweCI+PHRleHQgeD0iMTEzLjUiIHk9IjI3Ni41Ij5NUVRULkNvb2wgQVBJPC90ZXh0PjwvZz48cGF0aCBkPSJNIDE4OS42NiAyNjcuNjYgTCAyMzcuMzQgMjIzLjM0IiBmaWxsPSJub25lIiBzdHJva2U9IiMyYTVlNzQiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9Im5vbmUiLz48cGF0aCBkPSJNIDE4NS44MiAyNzEuMjQgTCAxODguNTYgMjYzLjkxIEwgMTg5LjY2IDI2Ny42NiBMIDE5My4zMyAyNjkuMDQgWiIgZmlsbD0iIzJhNWU3NCIgc3Ryb2tlPSIjMmE1ZTc0IiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJub25lIi8+PHBhdGggZD0iTSAyNDEuMTggMjE5Ljc2IEwgMjM4LjQ0IDIyNy4wOSBMIDIzNy4zNCAyMjMuMzQgTCAyMzMuNjcgMjIxLjk2IFoiIGZpbGw9IiMyYTVlNzQiIHN0cm9rZT0iIzJhNWU3NCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0ibm9uZSIvPjxyZWN0IHg9IjQ3NyIgeT0iMTcyIiB3aWR0aD0iMTg3IiBoZWlnaHQ9IjM1IiByeD0iNS4yNSIgcnk9IjUuMjUiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzMyOTZjMCIgc3Ryb2tlLXdpZHRoPSIyIiBwb2ludGVyLWV2ZW50cz0ibm9uZSIvPjxnIGZpbGw9IiNGRkZGRkYiIGZvbnQtZmFtaWx5PSJIZWx2ZXRpY2EiIHRleHQtYW5jaG9yPSJtaWRkbGUiIGZvbnQtc2l6ZT0iMTRweCI+PHRleHQgeD0iNTY5LjUiIHk9IjE5My41Ij5NUVRUIENvbm5lY3RvcjwvdGV4dD48L2c+PHJlY3QgeD0iNTAwIiB5PSI4MCIgd2lkdGg9IjE0MiIgaGVpZ2h0PSI0NyIgZmlsbD0iIzMyOTZjMCIgc3Ryb2tlPSJub25lIiBwb2ludGVyLWV2ZW50cz0ibm9uZSIvPjxnIGZpbGw9IiNGRkZGRkYiIGZvbnQtZmFtaWx5PSJIZWx2ZXRpY2EiIHRleHQtYW5jaG9yPSJtaWRkbGUiIGZvbnQtc2l6ZT0iMTRweCI+PHRleHQgeD0iNTcwLjUiIHk9IjEwOCI+SG9vayBQbHVnLWluPC90ZXh0PjwvZz48cmVjdCB4PSI1MDAiIHk9IjEyNyIgd2lkdGg9IjE0MiIgaGVpZ2h0PSI0MCIgZmlsbD0iIzU5YTJjMCIgc3Ryb2tlPSJub25lIiBwb2ludGVyLWV2ZW50cz0ibm9uZSIvPjxnIGZpbGw9IiNGRkZGRkYiIGZvbnQtZmFtaWx5PSJIZWx2ZXRpY2EiIHRleHQtYW5jaG9yPSJtaWRkbGUiIGZvbnQtc2l6ZT0iMTRweCI+PHRleHQgeD0iNTcwLjUiIHk9IjE1MS41Ij5Ib29rIEFQSTwvdGV4dD48L2c+PC9nPjwvc3ZnPg==)

</div>

<div class="title">

Figure 1. Architecture overview

</div>

</div>

<div class="paragraph">

MQTT.Cool embeds the high-performance Lightstreamer Engine to deliver
real-time data through the Internet, achieving low latency and high
scalability.

</div>

<div class="paragraph">

The MQTT Connector can connect to any MQTT broker to send and receive
MQTT messages to and from topics and to encapsulate them into
Lightstreamer’s internal protocol.

</div>

<div class="paragraph">

The *Hook Plug-in* enables you to add custom authentication and
authorization through the provided *Hook API*.

</div>

<div class="admonitionblock tip">

  ---- ---------------------------------------------------------------------------------
  **   Base knowledge of the MQTT protocol is required to fully understand this guide.
  ---- ---------------------------------------------------------------------------------

</div>

</div>

<div class="sect2">

### 1.3. Quick Start {#_quick_start}

<div class="paragraph">

This section will guide you through the installation of MQTT.Cool, to
get it up and running in very short time.

</div>

<div class="sect3">

#### 1.3.1. Check System Requirements {#_check_system_requirements}

<div class="paragraph">

MQTT.Cool requires a Java Virtual Machine. You can use either OpenJDK or
Oracle Java Platform, Standard Edition (either the Server JRE or the
JDK). Minimum supported Java version is 7, but newer versions are
recommended.

</div>

</div>

<div class="sect3">

#### 1.3.2. Download and Install {#_download_and_install}

<div class="paragraph">

[Download](http://www.lightstreamer.com/download.htm) the latest
MQTT.Cool package for your operating system.

</div>

<div class="paragraph">

On Mac or Unix-based systems, unpack the tarball:

</div>

<div class="listingblock">

<div class="content">

    $ tar -xvfz mqtt.cool_X_Y_Z_YYYYMMDD.tar.gz

</div>

</div>

<div class="paragraph">

The `mqtt.cool` directory will be created.

</div>

<div class="paragraph">

On Windows systems, extract the *mqtt.cool\_X\_Y\_Z\_YYYYMMDD.zip*
archive using your preferred tool into a directory of your choice (a
short base path is recommended, e.g. "C:\\"). The `mqtt.cool` directory
will be created.

</div>

</div>

<div class="sect3">

#### 1.3.3. Configure {#_configure}

<div class="paragraph">

Modify a few factory settings of the MQTT.Cool configuration:

</div>

<div class="sect4">

##### Choose TCP ports {#tcp}

<div class="paragraph">

By default, MQTT.Cool listens on TCP ports 8080 and 8888, but you may
change them by opening the `mqtt.cool/conf/lightstreamer_conf.xml` file
and editing the following elements:

</div>

<div class="ulist">

-   ***&lt;port&gt;*** inside the *&lt;http\_server&gt;* block

-   ***&lt;port&gt;*** inside the *&lt;rmi\_connector&gt;* block.

</div>

</div>

<div class="sect4">

##### Set JAVA\_HOME {#_set_java_home}

<div class="paragraph">

Edit the launch script in order to point to your JRE or JDK
installation:

</div>

<div class="ulist">

-   on Mac or Unix-based systems, open the **mc.sh** file under the
    `mqtt.cool/bin/unix-like` directory

-   on Windows systems, open the **mc.bat** file under the
    `mqtt.cool\bin\windows` directory

</div>

<div class="paragraph">

and set the value of the `JAVA_HOME` variable defined at the top of the
script according to your environment.

</div>

</div>

</div>

<div class="sect3">

#### 1.3.4. Attach an MQTT Broker {#_attach_an_mqtt_broker}

<div class="paragraph">

Before starting MQTT.Cool, a target MQTT broker to which to connect
should be up and running, otherwise no client connections can be
accepted.

</div>

<div class="paragraph">

MQTT.Cool comes with a set of predefined configurations for connecting
with local MQTT server instances, as well as with the most common
publicly accessible brokers. If you want to provide a new custom
configuration, open the `mqtt.cool/conf/mqtt_master_connector_conf.xml`
file and provide a set of entries similar to the following:

</div>

<div class="listingblock">

<div class="content">

``` {.CodeRay .highlight}
<!-- MQTT broker connection parameters for a local instance
     listening on port 1883, aliased by "mybroker". -->
<param name="mybroker.server_address">tcp://localhost:1883</param>
<param name="mybroker.connection_timeout">5</param>
<param name="mybroker.keep_alive">20</param>
```

</div>

</div>

<div class="paragraph">

As you can see, the connection parameters for a specific configuration
share a common prefix, which is the *connection alias* to be used by the
clients to specify the MQTT broker to connect to.

</div>

<div class="paragraph">

Now, start your MQTT broker, or ensure it is already running.

</div>

</div>

<div class="sect3">

#### 1.3.5. Start {#_start}

<div class="paragraph">

To launch MQTT.Cool:

</div>

<div class="ulist">

-   on Mac or Unix-based systems:

</div>

<div class="listingblock">

<div class="content">

    $ cd bin/unix-like
    $ ./start.sh

</div>

</div>

<div class="ulist">

-   on Windows systems: go to the `bin\windows` directory and execute
    `start_mc_as_application.bat`.

</div>

</div>

<div class="sect3">

#### 1.3.6. Check {#_check}

<div class="paragraph">

To verify whether the server has started correctly, open your browser to
`http://localhost:8080` (change the port according to [Section 1.3.3.1,
“Choose TCP ports”](#tcp)) and watch the Welcome page:

</div>

<div id="welcomepage" class="imageblock" style="text-align: center">

<div class="content">

![welcome
full](data:image/png;base64,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RERERERERERERNRiGAARERERERERERERERG1GAZARERERERERERERERELYYBEBERERERERERERERUYthAERERERERERERERERNRiGAARERERERERERERERG1GAZARERERERERERERERELYYBEBERERERERERERERUYthAERERERERERERERERNRiGAARERERERERERERERG1GAZARERERERERERERERELYYBEBERERERERERERERUYthAERERERERERERERERNRiGAARERERERERERERERG1GAZARERERERERERERERELYYBEBERERERERERERERUYthAERERERERERERERERNRiGAARERERERERERERERG1GAZARERERERERERERERELYYBEBERERERERERERERUYthAERERERERERERERERNRiGAARERERERERERERERG1GAZARERERERERERERERELYYBEBERERERERERERERUYthAERERERERERERERERNRiGAARERERERERERERERG1GAZARERERERERERERERELYYBEBERERERERERERERUYthAERERERERERERERERNRiGAARERERERERERERERG1GAZARERERERERERERERELYYBEBERERERERERERERUYthAERERERERERERERERNRiGAARERERERERERERERG1GAZARERERERERERERERELUbiIaC95BtnT/MgEBERERERERHRvvbzqzd4EIjomRgAET/ciIiIiIiIiIiIiIhaDEvAERERERERERERERERtRgGQERERERERERERERERC2GARAREREREREREREREVGLYQBERERERERERERERETUYhgAERERERERERERERERtRgGQERERERERERERERERC2GARAREREREREREREREVGLYQBERERERERERERERETUYhgAERERERERERERERERtRgGQERERERERERERERERC2GARAREREREREREREREVGLYQBERERERERERERERETUYhgAERERERERERERERERtRgGQERERERERERERERERC2GARAREREREREREREREVGLYQBERERERERERERERETUYhgAERERERERERERERERtRgGQERERERERERERERERC2GARAREREREREREREREVGLYQBERERERERERERERETUYhgAERERERERERERERERtRgGQERERERERERERERERC2GARAREREREREREREREVGLYQBERERERERERERERETUYhgAERERERERERERERERtRgGQERERERERERERERERC2GARAREREREREREREREVGLYQBERERERERERERERETUYhgAERERERERERERERERtRgGQERERERERERERERERC2GARAREREREREREREREVGLYQBERERERERERERERETUYhgAEdH+EhnG37z/S/zNUJTHgohoV4vi6vu/xN/80y2EeTCIiIiIiIiInpvEQ0CtRk7FcH9iAmNzcURyJcSqK1tE+CxWBD1t6D/UjaPtdkgCj9e+Uy1iPl8CyrVd+fSy9z7EXw1ngK4z+IsvBfflS/T4GADoH3wLf3zcvvFfTo/ihx+MYAwWvPO1t3HG+wLnkPAQvv9JBEmhHX/8P7yOfsM+ewHCQ/jLTyL1/zZ243v/8iQCmz1XKlF8/I/XcKkMAHa8+85bOOXY6C/XUFyaw/2JWYzNJbFYetHzegQXfzSEq5s+QHb83gDwy9HM5o/1Zt/n1RJi4SmMTUZwJ5FBrFiDvHKBJxnhc7hworMT/X0d8Fn24j0/NWTyJcyj0pwx7TiCP3tnADZ+EhI1ycp59XnP60REREREtF0YAFHLKC6M4tKnoxjKa03s1xDLZxDLZzAcHgd0Rpw59grOH/PBxCCIqDU4BnD+4DjGxvO4eGsCg7/bB9Pz/L6SwM2bESQB9A8e23/hz9NK07gxdQLv9G4uPJCnJnG5/GLn9YtXRnCziA2e1+04f+Z1vNFrae3XpZrHxPVr+MlkBllF45jLJczHo5iPR3Fx+AZszm58640T6LNx8TftT9nRK3jvdgzuY895YwEREREREdEexgCI9j6lhPDnV/B3DzMoAoAgoj80gLNHQgjaTTAZlie7lBqKpQySU2HceDSBm6kSbobj+MpxH4/hDpFLKcTiInxBe4ufjGqQsynMlywIeY184Z+Dz/n8k3SBl4/jzKNbGFocweVwDy6ENj7hXRy7i4s5ANaDuHB0n08QCoCkAEOjEzjfe/D5grQ1Srg/Gn28MmXD5/XrH+O98Xz993RGDPYdwrmDIbjsRphWThhKDcVcCpGpCdwcC2O4mMGlT3+NO48G8Sdv9cG1JtwP4sIfvYsL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aj0dTxUTEZFX1wieuz4GgNqtxRgUEBERERF5RSkBJJKsnnZx9lIbHUDta+V68lFEkv4jTfHeOo5tAiJd/D8XWhnQfkAiIq+kgdtXONkFZJTx5lZ95RURERGRV5cehhJJJqMjDD8J0XX/R76504V3FGxbanm/JF2xEZHkl5JJ9dsVNP9bC55wP/1PIMussIiIvAqikQih/g6a3T9yvjdCNMXKsQM7saUoNiIiIiLy6lICSGRdCuM+8yc+X3Cv81RKSnZz/M0CXegi8uqwlnPiUCYD1gJsGxQOST4mo7azl1fcw0b+7psOogt9yTXZOPZ2LdVWhUtEREREXm0aFxZZl8xkW4BnEkAGgxHbpixeL3JQuaOALF3hIvIqfrjJLcCmMEjSKeD9/3iM9xUIedVlWigBPDN+mIrNnEFBjh1X5Xacm42Kk4iIiIgIkPIvf7ykFfJFRERERERERERERESSiHbEFBERERERERERERERSTJKAImIiIiIiIiIiIiIiCQZJYBERERERERERERERESSjBJAIiIiIiIiIiIiIiIiSUYJIBERERERERERERERkSSjBJCIiIiIiIiIiIiIiEiSUQJIREREREREREREREQkySgBJCIiIiIiIiIiIiIikmSUABIREREREREREREREUkySgCJiIiIiIiIiIiIiIgkGSWAREREREREREREREREkowSQCIiIiIiIiIiIiIiIklGCSAREREREREREREREZEkowSQiIiIiIiIiIiIiIhIklECSEREREREREREREREJMkoASQiIiIiIiIiIiIiIpJklAASERERERERERERERFJMkoAiYiIiIiIiIiIiIiIJBklgERERERERERExzngZgAAIABJREFURERERJKMEkAiIiIiIiIiIiIiIiJJRgkgERERERERERERERGRJKMEkIiIiIiIiIiIiIiISJJRAkhERERERERERERERCTJKAEkIiIiIiIiIiIiIiKSZJQAEhERERERERERERERSTJKAImIiIiIiIiIiIiIiCQZJYBERERERERERERERESSjKH5wUNFQUREREREREREREREJIloBpCIiIiIiIiIiIiIiEiSUQJIREREREREREREREQkySgBJCIiIiIiIiIiIiIikmSUABIREREREREREREREUkySgCJiIiIiIiIiIiIiIgkGSWAREREREREREREREREkowSQCIiIiIiIiIiIiIiIklGCSAREREREREREREREZEkowSQiIiIiIiIiIiIiIhIklECSEREREREREREREREJMkoASQiIiIiIiIiIiIiIpJklAASERERERERERERERFJMkoAiYiIiIiIiIiIiIiIJBklgERERERERERERERERJKMEkAiIiIiIiIiIiIiIiJJRgkgERERERERERERERGRJKMEkIiIiIiIiIiIiIiISJJRAkhERERERERERERERCTJKAEkIiIiIiIiIiIiIiKSZJQAEhERERERERERERERSTJKAImIiIiIiIiIiIiIiCQZJYBERERERERERERERESSjBJAIiIiIiIiIiIiIiIiSUYJIBERERERERERERERkSRjUAhERETkpat9j1+WWOb//XiQhv91iYurWYby/fz1bhsh7+/5bf1aDFIZJ/59FY50YOAe/3TWTXDB1zs4fmwXpSaI+O/w3y+2zX5JzjaOvF5CeY4ZoyH+XND4GJHhMN1dXi423MM/+eJd/OyEg82JFDUyTMRowpjIS+cr2wRLEXW7ynDZM8lIn17GQdpbbnLaE1z90K/5tvEqi18XBLj4/12lQQFZliMffITL9OrF0O7cxcHSPPIsRoxp8R+OjjAU6qe1tYVz3uCs+1Rvgv1AzcE/56AdfDf+jZOt870q3q8O+vj7r26qbxIRERGRFacEkIiIiKx90RFCisKULDt1eXC6e4HXVDlwmOb/demuOo6UZ5OR8swvUlIxbrTgKHXxSUEely9cp+ElBd+6Yy8nXrNjTZurjFYqqw9gz7rMb+v71SZEZAnsHDy0mxrbHGnqtHQyrHaqa204bI38tr5L4RIRERGRdUsJIBEREVkzevUU8+KiY0QNZhzlDuj2zfMiM4eLszFEx4ga5ljxt3w/R3dkYwSiQ/00t7fR/KALXwis9gIqHWW4tmZj3Win7p1d9H11k3Zu8tuTM59QT+wJ95gjH3yEKzOE++QFziRynoW7OD6R/BkJ4fmxjSavD18IyLFTXeTA5TDR7VPyR0SWwkzNwT3U2NKBMYb6unHf99Hq8eMn3gcWOSgvNtP7cFryp/4Cf6/7k4iIiIisM0oAiYiIiKwnT4L4N2ZTmOtgHz6uzfWavApKsyAaCBK0ZTNzcT0bR7fbMBJbfu3Ti20zlpIL+ru45u/iWruTT96t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)

</div>

<div class="title">

Figure 2. The Welcome page

</div>

</div>

</div>

</div>

<div class="sect2">

### 1.4. Hello IoT World Tutorial {#_hello_iot_world_tutorial}

<div class="paragraph">

Now it is time to "get your hands dirty" through a quick tutorial, which
will let you build a full end-to-end example.

</div>

<div class="paragraph">

In the following diagram the general flow we are going to implement:

</div>

<div class="imageblock" style="text-align: center">

<div class="content">

![tutorial](data:image/svg+xml;base64,PCFET0NUWVBFIHN2ZyBQVUJMSUMgIi0vL1czQy8vRFREIFNWRyAxLjEvL0VOIiAiaHR0cDovL3d3dy53My5vcmcvR3JhcGhpY3MvU1ZHLzEuMS9EVEQvc3ZnMTEuZHRkIj4KPHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHhtbG5zOnhsaW5rPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hsaW5rIiB3aWR0aD0iOTAxcHgiIGhlaWdodD0iMzExcHgiIHZlcnNpb249IjEuMSIgc3R5bGU9ImJhY2tncm91bmQtY29sb3I6IHJnYigyNTUsIDI1NSwgMjU1KTsiPjxkZWZzLz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgwLjUsMC41KSI+PHJlY3QgeD0iMCIgeT0iMCIgd2lkdGg9IjkwMCIgaGVpZ2h0PSIzMTAiIGZpbGw9IiNmZmZmZmYiIHN0cm9rZT0ibm9uZSIgcG9pbnRlci1ldmVudHM9Im5vbmUiLz48cmVjdCB4PSI2MCIgeT0iMjEwIiB3aWR0aD0iMTI0IiBoZWlnaHQ9IjYwIiBmaWxsPSIjMzI5NmMwIiBzdHJva2U9Im5vbmUiIHBvaW50ZXItZXZlbnRzPSJub25lIi8+PGcgZmlsbD0iI0ZGRkZGRiIgZm9udC1mYW1pbHk9IkhlbHZldGljYSIgdGV4dC1hbmNob3I9Im1pZGRsZSIgZm9udC1zaXplPSIxMnB4Ij48dGV4dCB4PSIxMjEuNSIgeT0iMjM2LjUiPkphdmFTY3JpcHQgQ2xpZW50PC90ZXh0Pjx0ZXh0IHg9IjEyMS41IiB5PSIyNTAuNSI+aW4gSFRNTCBwYWdlPC90ZXh0PjwvZz48cmVjdCB4PSI3OTAiIHk9IjkyIiB3aWR0aD0iODAiIGhlaWdodD0iNDAiIGZpbGw9IiM3NDUyMmEiIHN0cm9rZT0ibm9uZSIgcG9pbnRlci1ldmVudHM9Im5vbmUiLz48ZyBmaWxsPSIjRkZGRkZGIiBmb250LWZhbWlseT0iSGVsdmV0aWNhIiB0ZXh0LWFuY2hvcj0ibWlkZGxlIiBmb250LXNpemU9IjEycHgiPjx0ZXh0IHg9IjgyOS41IiB5PSIxMDguNSI+SmF2YTwvdGV4dD48dGV4dCB4PSI4MjkuNSIgeT0iMTIyLjUiPk1RVFQgQ2xpZW50PC90ZXh0PjwvZz48cGF0aCBkPSJNIDYwNy4zNyAxMTIgTCA3OTAgMTEyIiBmaWxsPSJub25lIiBzdHJva2U9IiNjMDc1MWYiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgc3Ryb2tlLWRhc2hhcnJheT0iMSAxIiBwb2ludGVyLWV2ZW50cz0ibm9uZSIvPjxwYXRoIGQ9Ik0gNjAyLjEyIDExMiBMIDYwOS4xMiAxMDguNSBMIDYwNy4zNyAxMTIgTCA2MDkuMTIgMTE1LjUgWiIgZmlsbD0iI2MwNzUxZiIgc3Ryb2tlPSIjYzA3NTFmIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJub25lIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoNjIzLjUsOTUuNSkiPjxzd2l0Y2g+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OnZpc2libGU7IiBwb2ludGVyLWV2ZW50cz0iYWxsIiB3aWR0aD0iMTQ1IiBoZWlnaHQ9IjEzIiByZXF1aXJlZEZlYXR1cmVzPSJodHRwOi8vd3d3LnczLm9yZy9UUi9TVkcxMS9mZWF0dXJlI0V4dGVuc2liaWxpdHkiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTNweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6IHJnYigxOTIsIDExNywgMzEpOyBsaW5lLWhlaWdodDogMS4yOyB2ZXJ0aWNhbC1hbGlnbjogdG9wOyB3aGl0ZS1zcGFjZTogbm93cmFwOyBmb250LXdlaWdodDogYm9sZDsgdGV4dC1hbGlnbjogY2VudGVyOyI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6aW5saW5lLWJsb2NrO3RleHQtYWxpZ246aW5oZXJpdDt0ZXh0LWRlY29yYXRpb246aW5oZXJpdDsiPlB1Ymxpc2ggdG8gTVFUVCB0b3BpY3M8L2Rpdj48L2Rpdj48L2ZvcmVpZ25PYmplY3Q+PHRleHQgeD0iNzMiIHk9IjEzIiBmaWxsPSIjQzA3NTFGIiB0ZXh0LWFuY2hvcj0ibWlkZGxlIiBmb250LXNpemU9IjEzcHgiIGZvbnQtZmFtaWx5PSJIZWx2ZXRpY2EiIGZvbnQtd2VpZ2h0PSJib2xkIj5QdWJsaXNoIHRvIE1RVFQgdG9waWNzPC90ZXh0Pjwvc3dpdGNoPjwvZz48cGF0aCBkPSJNIDQzNi4zNyAxMTIgTCA0OTMuNjMgMTEyIiBmaWxsPSJub25lIiBzdHJva2U9IiMyYTVlNzQiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgc3Ryb2tlLWRhc2hhcnJheT0iMSAxIiBwb2ludGVyLWV2ZW50cz0ibm9uZSIvPjxwYXRoIGQ9Ik0gNDMxLjEyIDExMiBMIDQzOC4xMiAxMDguNSBMIDQzNi4zNyAxMTIgTCA0MzguMTIgMTE1LjUgWiIgZmlsbD0iIzJhNWU3NCIgc3Ryb2tlPSIjMmE1ZTc0IiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJub25lIi8+PHBhdGggZD0iTSA0OTguODggMTEyIEwgNDkxLjg4IDExNS41IEwgNDkzLjYzIDExMiBMIDQ5MS44OCAxMDguNSBaIiBmaWxsPSIjMmE1ZTc0IiBzdHJva2U9IiMyYTVlNzQiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9Im5vbmUiLz48cGF0aCBkPSJNIDM1NSAxNjIgUSAzNTUgMjQwIDE5MC4zNyAyNDAiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzJhNWU3NCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBzdHJva2UtZGFzaGFycmF5PSIxIDEiIHBvaW50ZXItZXZlbnRzPSJub25lIi8+PHBhdGggZD0iTSAxODUuMTIgMjQwIEwgMTkyLjEyIDIzNi41IEwgMTkwLjM3IDI0MCBMIDE5Mi4xMiAyNDMuNSBaIiBmaWxsPSIjMmE1ZTc0IiBzdHJva2U9IiMyYTVlNzQiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9Im5vbmUiLz48ZyBmaWxsPSIjMkE1RTc0IiBmb250LWZhbWlseT0iSGVsdmV0aWNhIiBmb250LXdlaWdodD0iYm9sZCIgdGV4dC1hbmNob3I9Im1pZGRsZSIgZm9udC1zaXplPSIxM3B4Ij48dGV4dCB4PSIyNjIuNSIgeT0iMjA2Ij5SZWNlaXZlwqA8L3RleHQ+PHRleHQgeD0iMjYyLjUiIHk9IjIyMiI+dGVsZW1ldHJ5IGRhdGE8L3RleHQ+PC9nPjxwYXRoIGQ9Ik0gMTMwIDIxMCBRIDEzMCAxMTQgMjczLjYzIDExNCIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMmE1ZTc0IiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHN0cm9rZS1kYXNoYXJyYXk9IjEgMSIgcG9pbnRlci1ldmVudHM9Im5vbmUiLz48cGF0aCBkPSJNIDI3OC44OCAxMTQgTCAyNzEuODggMTE3LjUgTCAyNzMuNjMgMTE0IEwgMjcxLjg4IDExMC41IFoiIGZpbGw9IiMyYTVlNzQiIHN0cm9rZT0iIzJhNWU3NCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0ibm9uZSIvPjxnIGZpbGw9IiMyQTVFNzQiIGZvbnQtZmFtaWx5PSJIZWx2ZXRpY2EiIGZvbnQtd2VpZ2h0PSJib2xkIiB0ZXh0LWFuY2hvcj0ibWlkZGxlIiBmb250LXNpemU9IjEzcHgiPjx0ZXh0IHg9IjE2MS41IiB5PSI5OSI+U3Vic2NyaWJlIHRvPC90ZXh0Pjx0ZXh0IHg9IjE2MS41IiB5PSIxMTUiPk1RVFQgdG9waWNzPC90ZXh0PjwvZz48cmVjdCB4PSIyODAiIHk9IjY2IiB3aWR0aD0iMTUwIiBoZWlnaHQ9Ijk2IiByeD0iMTQuNCIgcnk9IjE0LjQiIGZpbGw9IiMyYTVlNzQiIHN0cm9rZT0ibm9uZSIgcG9pbnRlci1ldmVudHM9Im5vbmUiLz48ZyBmaWxsPSIjRkZGRkZGIiBmb250LWZhbWlseT0iSGVsdmV0aWNhIiB0ZXh0LWFuY2hvcj0ibWlkZGxlIiBmb250LXNpemU9IjE3cHgiPjx0ZXh0IHg9IjM1NC41IiB5PSIxMjAiPk1RVFQuQ29vbDwvdGV4dD48L2c+PHJlY3QgeD0iNTAwIiB5PSI3MiIgd2lkdGg9IjEwMCIgaGVpZ2h0PSI4MCIgcng9IjEyIiByeT0iMTIiIGZpbGw9IiNjMDc1MWYiIHN0cm9rZT0ibm9uZSIgcG9pbnRlci1ldmVudHM9Im5vbmUiLz48ZyBmaWxsPSIjRkZGRkZGIiBmb250LWZhbWlseT0iSGVsdmV0aWNhIiB0ZXh0LWFuY2hvcj0ibWlkZGxlIiBmb250LXNpemU9IjE3cHgiPjx0ZXh0IHg9IjU0OS41IiB5PSIxMDgiPk1RVFTCoDwvdGV4dD48dGV4dCB4PSI1NDkuNSIgeT0iMTI4Ij5Ccm9rZXI8L3RleHQ+PC9nPjwvZz48L3N2Zz4=)

</div>

<div class="title">

Figure 3. General flow for the example

</div>

</div>

<div class="paragraph">

A JavaScript application, running inside the browser, subscribes to two
MQTT topics, in order to *consume* real-time telemetry metrics like
*speed* and *engine RPM* from a hypothetical car; upon receiving, data
messages are displayed on the HTML page.

</div>

<div class="paragraph">

Real-time telemetry updates are delivered by a random feed simulator,
which is a pure MQTT Java client that connects to the MQTT broker,
generates simulated data and *publishes* them to the target topics at a
fixed interval (100 ms).

</div>

<div class="admonitionblock note">

  ---- --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  **   This example is a *light* version of the [Hello IoT World](https://github.com/MQTTCool/MQTT.Cool-example-Hello_IoT_World-client-javascript) example available on GitHub, where also graphical gauges are employed.
  ---- --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

</div>

<div class="sect3">

#### 1.4.1. Step 1: Setup an MQTT Broker {#_step_1_setup_an_mqtt_broker}

<div class="paragraph">

First of all, we need an up and running MQTT broker to which clients can
connect to for messages exchange.

</div>

<div class="paragraph">

To keep things simple, let’s configure a broker on the same machine on
which MQTT.Cool has been already installed so that no particular network
setup will be needed to make the two servers talk each other.

</div>

<div class="paragraph">

We suggest using [Mosquitto](http://mosquitto.org), as it is very easy
to configure and run, besides being one of the most popular and widely
used open source MQTT brokers.

</div>

<div class="admonitionblock note">

  ---- ------------------------------------------------------------------------------------------------------------------------------------------------
  **   For the purpose of the tutorial, there is no requirement to use a specific MQTT broker, therefore feel free to use your preferred MQTT broker.
  ---- ------------------------------------------------------------------------------------------------------------------------------------------------

</div>

<div class="paragraph">

[Download](http://mosquitto.org/downloads) and install the binary
package according to your system.

</div>

<div class="paragraph">

As default configuration is ok for our goals (no authentication required
and service will listen on default TCP port 1883), simply start the
broker:

</div>

<div class="ulist">

-   on Mac or Linux systems:

</div>

<div class="listingblock">

<div class="content">

    $ mosquitto

</div>

</div>

<div class="ulist">

-   on Windows systems: go to the Mosquitto installation directory and
    execute `mosquitto.exe`

</div>

<div class="admonitionblock tip">

  ---- ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  **   If you are familiar with Docker, you might also want to install and run the [official image](https://store.docker.com/images/eclipse-mosquitto). Please also consider that you could use one of the public test brokers available for development and testing purposes: [here](https://github.com/mqtt/mqtt.github.io/wiki/public_brokers) an up-to-date list.
  ---- ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

</div>

</div>

<div class="sect3">

#### 1.4.2. Step 2: Attach the MQTT Broker {#_step_2_attach_the_mqtt_broker}

<div class="paragraph">

After having configured and started the broker, you need to ensure that
MQTT.Cool can contact it upon a connection request coming from any
client.

</div>

<div class="paragraph">

MQTT.Cool comes with a set of predefined configurations for connecting
with local MQTT server instances, as well as with the most common
publicly accessible brokers. They are defined in the
`mqtt.cool/conf/mqtt_master_connector_conf.xml` file through sets of
entries similar to the following:

</div>

<div class="listingblock">

<div class="content">

``` {.CodeRay .highlight}
<!-- MQTT broker connection parameters for a local instance
     listening on port 1883, aliased by "mybroker". -->
<param name="mybroker.server_address">tcp://localhost:1883</param>
<param name="mybroker.connection_timeout">5</param>
<param name="mybroker.keep_alive">20</param>
```

</div>

</div>

<div class="paragraph">

Basically, the connection parameters for a specific configuration share
a common prefix, which is the connection alias to be used by the clients
to specify the MQTT broker to connect to. More details on this will be
provided in [Section 2.1, “Static Lookup”](#static_lookup).

</div>

<div class="paragraph">

For the exercise, the following predefined configuration allows
MQTT.Cool to connect to the local Mosquitto server, therefore there is
no need to change default settings:

</div>

<div class="listingblock">

<div class="content">

``` {.CodeRay .highlight}
<!--
  =====================================
  CONFIGURATION EXAMPLE FOR "Mosquitto"
  =====================================
-->
<param name="mosquitto.server_address">tcp://localhost:1883</param>
<param name="mosquitto.clientid_prefix">mosquitto_client</param>
<param name="mosquitto.connection_timeout">30</param>
<param name="mosquitto.keep_alive">10</param>
```

</div>

</div>

</div>

<div class="sect3">

#### 1.4.3. Step 3: Write the Feed Simulator {#_step_3_write_the_feed_simulator}

<div class="paragraph">

As said, to simulate and publish telemetry information we will lean on a
Java client application, which is based on the [Eclipse Paho Java
Client](https://eclipse.org/paho/clients/java/), a largely used MQTT
client library for the JVM.

</div>

<div class="paragraph">

Let’s start with the code snippet relative to the application entry
point:

</div>

<div class="listingblock">

<div class="content">

``` {.CodeRay .highlight}
public static void main(String args[]) throws Exception {
  MqttClient client = new MqttClient("tcp://localhost:1883", "telemetry-feed"); (1)
  client.connect(); (2)

  ScheduledExecutorService executor = Executors.newSingleThreadScheduledExecutor();
  executor.scheduleAtFixedRate(new Feed(client), 0, 100, TimeUnit.MILLISECONDS); (3)
}
```

</div>

</div>

<div class="colist arabic">

  --------- --------------------------------------------------------------------------------------------------------------------------------------------------------------
  ****1**   Create a new client instanced targeted to the MQTT broker running on localhost and listening on TCP port 1883; the client is identified as `telemetry-feed`.
  ****2**   Connect and wait for response.
  ****3**   Once connected, schedule a task for generating and publishing telemetry data every 100 ms.
  --------- --------------------------------------------------------------------------------------------------------------------------------------------------------------

</div>

<div class="paragraph">

The task is implemented through an instance of the `Feed` class, which
produces *fake* data and sends them to the designated MQTT topics. Below
the code snippet for the `run` method:

</div>

<div class="listingblock">

<div class="content">

``` {.CodeRay .highlight}
public void run()
  long speedKmH = simulateSpeed(); (1)
  long rpm = simulateRPM(speedKmH); (2)

  try {
      client.publish("telemetry/speed", toBytes(speedKmH), 0, false); (3)
      client.publish("telemetry/rpm", toBytes(rpm), 0, false); (4)
  } catch (MqttException e) {
      e.printStackTrace();
  }
}
```

</div>

</div>

<div class="colist arabic">

  --------- --------------------------------------------------------
  ****1**   Calculate the simulated car speed.
  ****2**   Calculate the simulated car’s engine RPM.
  ****3**   Publish the speed data to the `telemetry/speed` topic.
  ****4**   Publish the RMP data to the `telemetry/rpm` topic.
  --------- --------------------------------------------------------

</div>

<div class="paragraph">

To recap, here how the full MQTT client application code should look
like:

</div>

<div class="listingblock">

<div class="content">

``` {.CodeRay .highlight}
import org.eclipse.paho.client.mqttv3.*;
import java.util.concurrent.*;

/** The feed task for publishing telemetry data at a fixed rate to the MQTT broker. */
public class Feed implements Runnable {

  /** Speed limit in Km/h to determine speed variation range */
  private static final int SPEED_LIMIT_KMH = 135;

  /** Base speed limit to determine speed variation range */
  private static final int BASE_SPEED_KMH = 215;

  /** RPM base value */
  private static final int BASE_RPM = 2000;

  /** Fixed thresholds to determine RPM calculation */
  private static final int[] GEAR_THRESHOLDS = { 90, 150, 220, 300, 320 };

  /** Gear ratios to determine RPM calculation */
  private static final int[] GEAR_RATIOS = { 250, 400, 300, 250, 1000, 660 };

  /** Initial simulated speed in Km/h, also to used to save last determined speed */
  private long lastSpeedKmH = 130;

  /** Reference to the MqttClient instance connected to the MQTT broker */
  private MqttClient client;

  Feed(MqttClient client) {
    this.client = client;
  }

  /**
   * Utility method for converting a long value into a string representation to be
   * used as message payload.
   *
   * @param value
   * @return
   */
  static byte[] toBytes(long value) {
    return String.valueOf(value).getBytes();
  }

  @Override
  public void run() {
    long speedKmH = simulateSpeed();
    long rpm = simulateRPM(speedKmH);

    // Publish data to the MQTT broker
    try {
      client.publish("telemetry/speed", toBytes(speedKmH), 0, false);
      client.publish("telemetry/rpm", toBytes(rpm), 0, false);
    } catch (MqttException e) {
      e.printStackTrace();
    }
  }

  /**
   * Calculates and returns the simulated speed.
   *
   * @return the speed
   */
  long simulateSpeed() {
    // Simulate the speed variation
    double ratio = (double) (lastSpeedKmH - BASE_SPEED_KMH) / SPEED_LIMIT_KMH;
    int direction = 1;
    if (ratio < 0) {
      direction = -1;
    }
    ratio = Math.min(Math.abs(ratio), 1);
    double weight = (ratio * ratio * ratio);
    double prob = (1 - weight) / 2;
    if (!(Math.random() < prob)) {
      direction = direction * -1;
    }
    long difference = Math.round(Math.random() * 3) * direction;

    // Get current speed and save it for next simulation
    long speedKmH = lastSpeedKmH + difference;
    lastSpeedKmH = speedKmH;
    return speedKmH;
  }

  /**
   * Calculate and returns the simulated engine RPM.
   *
   * @return the RPM
   */
  long simulateRPM(long speedKmH) {
    // Calculate current RPM
    long diff = speedKmH;
    int i = 0;
    for (i = 0; i < GEAR_THRESHOLDS.length; i++) {
      if (speedKmH < GEAR_THRESHOLDS[i]) {
        break;
      }
    }
    if (i > 0) {
      diff = speedKmH - GEAR_THRESHOLDS[i - 1];
    }
    return BASE_RPM + GEAR_RATIOS[i] * diff;
  }

  public static void main(String[] args) throws MqttException {
    // Create a client connection to the MQTT broker running on localhost
    // and listening on TCP port 1883
    MqttClient client = new MqttClient("tcp://localhost:1883", "telemetry-feed");
    client.connect();

    // Once connected, generate and publish simulated telemetry data every 100 ms
    ScheduledExecutorService executor = Executors.newSingleThreadScheduledExecutor();
    executor.scheduleAtFixedRate(new Feed(client), 0, 100, TimeUnit.MILLISECONDS);
  }
}
```

</div>

</div>

<div class="paragraph">

From the development folder under which you are going to build the feed
example, execute the following easy steps (shown for a Linux system):

</div>

<div class="ulist">

-   Copy the code above into a new Java source file called `Feed.java`.

-   [Download](https://repo.eclipse.org/content/repositories/paho-releases/org/eclipse/paho/org.eclipse.paho.client.mqttv3/1.0.2/org.eclipse.paho.client.mqttv3-1.0.2.jar)
    the Paho Java Client jar file into a new `lib` directory.

-   Compile the source code:

    <div class="listingblock">

    <div class="content">

        $ javac -cp lib/org.eclipse.paho.client.mqttv3-1.0.2.jar Feed.java

    </div>

    </div>

-   Then start the Feed:

    <div class="listingblock">

    <div class="content">

        $ java -cp .:lib/org.eclipse.paho.client.mqttv3-1.0.2.jar Feed

    </div>

    </div>

</div>

<div class="paragraph">

From now on, the messages are periodically published to the MQTT broker.

</div>

<div class="admonitionblock tip">

  ---- -----------------------------------------------------------------------------------------------------------------------------------------------------------------
  **   As shown by the full example on GitHub, using a dependency management tool like Maven is a more practical way to include the Paho Java Client in your projects.
  ---- -----------------------------------------------------------------------------------------------------------------------------------------------------------------

</div>

</div>

<div class="sect3">

#### 1.4.4. Step 4: Make the JavaScript Client {#_step_4_make_the_javascript_client}

<div class="paragraph">

Let’s focus now on the most exciting part, which will lead us to run our
MQTT.Cool JavaScript client application!

</div>

<div class="paragraph">

Once again, since we aim at making our life easier, we are going to
embed the client code into a very simple HTML page, as follows:

</div>

<div class="listingblock">

<div class="content">

``` {.CodeRay .highlight}
<html>
<head>
  <title>Hello IoT World Tutorial</title>
  <script src="https://unpkg.com/mqtt.cool-web-client"></script> (1)

  <script>
    mqttcool.openSession('http://localhost:8080', { (2)

      onConnectionSuccess: function(mqttCoolSession) {
        var mqttClient = mqttCoolSession.createClient('mosquitto'); (3)

        mqttClient.onMessageArrived = onMessageArrived; (4)

        mqttClient.connect({ (5)
          onSuccess: function() {
            mqttClient.subscribe('telemetry/speed');
            mqttClient.subscribe('telemetry/rpm'); (6)
          }
        });

        function onMessageArrived(message) {
          var dest = message.destinationName;
          var rowId = dest.split('/', 2)[1]; (7)
          document.getElementById(rowId).innerHTML = message.payloadString; (8)
        }
      }
    });
  </script>
</head>
<body>
  <div>
    <div style="float: left;margin-right: 10px;">Speed</div><div id="speed"></div>
    <div style="float: left;margin-right: 10px;">RPM</div><div id="rpm"></div>
  </div>
</body>
</html>
```

</div>

</div>

<div class="colist arabic">

  --------- ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  ****1**   Load the MQTT.Cool JavaScript library file from the [`unpkg`](https://unpkg.com/#/) service.
  ****2**   Connect to the local MQTT.Cool server, listening on TPC port `8080`.
  ****3**   On successful connection, make a new [`MqttClient`](http://www.lightstreamer.com/api/mqtt.cool-web-client/latest/MqttClient.html) instance, ready to be connected to the Mosquitto server as configured in `mqtt_master_connector_conf.xml`.
  ****4**   Set the function callback to be triggered on messages arriving.
  ****5**   Connect to Mosquitto.
  ****6**   Upon successful `CONNACK`, subscribe to the designated MQTT topics.
  ****7**   Once a new message arrives, elaborate its topic name in order to retrieve the identifier relative to the `<div>` element to be updated.
  ****8**   Update the `<div>` element with the message payload.
  --------- ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

</div>

<div class="paragraph">

The `body` element simply contains the two `div` objects referenced by
the JavaScript code and periodically rendered with published telemetry
data. Their identifiers match the relevant part of the topics (e.g,
`telemetry/<metric>`), so that it is trivial to dispatch any message
payload to its pertinent visual object.

</div>

<div class="paragraph">

Finally, load the HTML page into the web browser, which should display
something similar to the following:

</div>

<div class="imageblock" style="text-align: center">

<div class="content">

![example
screenshot](data:image/png;base64,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AACAIAEAAACAIAEAAACAIAEAAACAIAEAAACAIAEAAAAABAkAAAAABAkAAAAABAkAAAAABAkAAAAABAkAAAAABAkAAAAAIEgAAAAAIEgAAAAAIEgAAAAAIEgAAAAAIEgAAAAAAEECAAAAAEECAAAAAEECAAAAAEECAAAAAEECAAAAAAgSAAAAAAgSAAAAAAgSAAAAAAgSAAAAAAgSAAAAAECQAAAAAECQAAAAAECQAAAAAECQAAAAAECQAAAAAECQAAAAAACCBAAAAACCBAAAAACCBAAAAACCBAAAAACCBAAAAAAQJAAAAAAQJAAAAAAQJAAAAAAQJAAAAAAQJAAAAACAIAEAAACAIAEAAACAIAEAAACAIAEAAACAIAEAAAAABAkAAAAABAkAAAAABAkAAAAABAkAAAAABAkAAAAABAkAAAAAIEgAAAAAIEgAAAAAIEgAAAAAIEgAAAAAIEgAAAAAAEECAAAAAEECAAAAAEECAAAAAEECAAAAAEECAAAAAAgSAAAAAAgSAAAAAAgSAAAAAAgSAAAAAAgSAAAAAAgSAAAAAECQAAAAAECQAAAAAECQAAAAAECQAAAAAECQAAAAAACCBAAAAACCBAAAAACCBAAAAACCBAAAAACCBAAAAAAQJAAAAAAQJAAAAAAQJAAAAAAQJAAAAAAQJAAAAACAIAEAAACAIAEAAACAIAEAAACAIAEAAACAIAEAAACAIAEAAAAABAkAAAAABAkAAAAABAkAAAAABAkAAAAABAkAAAAAIEgAAAAAIEgAAAAAIEgAAAAAIEgAAAAAIEgAAAAAAEECAAAAAEECAAAAAEECAAAAAEECAAAAAEECAAAAAAgSAAAAAAgSAAAAAAgSAAAAAAgSAAAAAAgSAAAAAAgSAAAAAECQAAAAAECQAAAAAECQAAAAAECQAAAAAECQAAAAAACCBAAAAACCBAAAAACCBAAAAACCBAAAAACCBAAAAAAQJAAAAAAQJAAAAAAQJAAAAAAQJAAAAAAQJAAAAACAIAEAAACAIAEAAACAIAEAAACAIAEAAACAIAEAAACAIAEAAAAABAkAAAAABAkAAAAABAkAAAAABAkAAAAABAkAAAAAIEgAAAAAIEgAAAAAIEgAAAAAIEgAAAAAIEgAAAAAAEECAAAAAEECAAAAAEECAAAAAEECAAAAAEECAAAAAEGCXQAAAACAIAEAAACAIAEAAACAIAEAAACAIAEAAACAIAEAAAAABAkAAAAABAkAAAAABAkAAAAABAkAAAAABAkAAAAAIEgAAAAAIEgAAAAAIEgAAAAAIEgAAAAAIEgAAAAAAEECAAAAAEECAAAAAEECAAAAAEECAAAAAEECAAAAAEECAAAAAAgSAAAAAAgSAAAAAAgSAAAAAAgSAAAAAAgSAAAAAECQAAAAAECQAAAAAECQAAAAAECQAAAAAECQAAAAAACCBAAAAACCBAAAAACCBAAAAACCBAAAAACCBAAAAAAQJAAAAAAQJAAAAAAQJAAAAAAQJAAAAAAQJAAAAAAQJAAAAACAIAEAAACAIAEAAACAIAEAAACAIAEAAACAIAEAAAAABAkAAAAABAkAAAAABAkAAAAABAkAAAAABAkAAAAAIEgAAAAAIEgAAAAAIEgAAAAAIEgAAAAAIEgAAAAAAEECAAAAAEECAAAAAEECAAAAAEECAAAAAEECAAAAAEECAAAAAAgSAAAAAAgSAAAAAAgSAAAAAAgSAAAAAAgSAAAAAECQAAAAAECQAAAAAECQAAAAAECQAAAAAECQAAAAAACCBAAAAACCBAAAAACCBAAAAACCBAAAAACCBAAAAAAQJAAAAAAQJAAAAAAQJAAAAAAQJAAAAAAQJAAAAAAQJAAAAACAIAEAAACAIAEAAACAIAEAAACAIAEAAACAIAEAAAAABAkAAAAABAkAAAAABAkAAAAABAkAAAAABAkAAAAAIEgAAAAAIEgAAAAAIEgAAAAAIEgAAAAAIEgAAAAAIEgAAAAAAEECAAAAAEECAAAAAEECAAAAAEECAAAAAEECAAAAAAgSAAAAAAgSAAAAAAgSAAAAAAgSAAAAAAgSAAAAAECQAAAAAECQAAAAAECQAAAAAECQAAAAAECQAAAAAACCBAAAAACCBAAAAACCBAAAAACCBAAAAACCBAAAAACCBAAAAAAQJAAAAAB0pwhJGvlABXsCAAAAQND+P/WA9M1bVAv1AAAAAElFTkSuQmCC)

</div>

<div class="title">

Figure 4. Example running into web browser

</div>

</div>

<div class="paragraph">

Just two last notes:

</div>

<div class="ulist">

-   The proposed tutorial is a gentle introduction to the entire
    MQTT.Cool ecosystem, hence most of the features have not been
    covered here: in the next sections, you will be provided with full
    information about server-side configuration and client-side
    development.

-   As already anticipated, the discussed end-to-end example is a
    simplified version of the [Hello IoT
    World](https://github.com/MQTTCool/MQTT.Cool-example-Hello_IoT_World-client-javascript)
    demo available on GitHub, which shows you a more sophisticated usage
    of the MQTT.Cool JavaScript library and other "cool" things…​

</div>

<div class="paragraph">

Final recommendation: enjoy MQTT messaging with MQTT.Cool!

</div>

</div>

</div>

</div>

</div>

<div class="sect1">

2. Addressing MQTT Brokers {#_addressing_mqtt_brokers}
--------------------------

<div class="sectionbody">

<div class="paragraph">

In this chapter, we will discuss two different approaches through which
a client can connect to an MQTT broker:

</div>

<div class="olist arabic">

1.  **Static Lookup**, by providing a reference to a static
    configuration already supplied in MQTT.Cool.

2.  **Dynamic Lookup**, by providing an explicit *URI* of the MQTT
    broker.

</div>

<div class="sect2">

### 2.1. Static Lookup {#static_lookup}

<div class="paragraph">

To activate the *Static Lookup*, a specific configuration for each
addressable MQTT broker has to be provided in the
`mqtt_master_connector_conf.xml` file. A configuration is given by the
set of connection parameters to be used for establishing the
communication from the MQTT.Cool server process to the target broker,
and is uniquely identified by a *connection alias*, which is the common
prefix embedded in each parameter name.

</div>

<div class="paragraph">

More specifically, you will define a configuration by providing entries
in the following form:

</div>

<div class="listingblock">

<div class="content">

``` {.CodeRay .highlight}
<param name="<connection_alias>.<connection_param_1>">.../param>
<param name="<connection_alias>.<connection_param_2>">.../param>
...
<param name="<connection_alias>.<connection_param_N>">.../param>
```

</div>

</div>

<div class="paragraph">

where:

</div>

<div class="ulist">

-   **&lt;connection\_alias&gt;** is the configuration identifier

-   **&lt;connection\_param\_J&gt;** is the J\_th connection parameter
    to be set for this configuration and which can be one of the
    following:

    <div class="ulist">

    -   `server_address`, the address of the MQTT broker to connect to

    -   `clientid_prefix`, the Client Id prefix to be used for *shared
        connections*, as will be detailed in [Section 3.6.3, “Shared
        End-to-End Connection”](#shared_connection)

    -   `connection_timeout`, the connection timeout

    -   `keep_alive`, the keep alive interval

    -   `username`, the username for authenticating with the MQTT broker

    -   `password`, the password for authenticating with the MQTT broker

    -   `will_message`, the Will Message payload

    -   `will_message_format`, the format of the Will Message payload

    -   `will_topic`, the Will Message topic name

    -   `will_qos`, the Will Message Quality of Service

    -   `will_retain`, the Will Message retain flag.

    </div>

</div>

<div class="admonitionblock tip">

  ---- -----------------------------------------------------------------------------------------------------------------------
  **   See [Appendix A, *Connection Parameters*](#_connection_parameters) for a more in-depth description of each parameter.
  ---- -----------------------------------------------------------------------------------------------------------------------

</div>

<div class="paragraph">

For example, a configuration for a local *Mosquitto* instance could be
provided by defining all the related parameters under the connection
alias `mosquitto`, as follows:

</div>

<div class="listingblock">

<div class="content">

``` {.CodeRay .highlight}
<param name="mosquitto.server_address">tcp://localhost:1883</param>
<param name="mosquitto.connection_timeout">5</param>
<param name="mosquitto.keep_alive">10</param>
...
```

</div>

</div>

<div class="paragraph">

The clients that want to connect to an MQTT broker for which a static
configuration has been provided on the server side, simply supply the
corresponding connection alias. Then, MQTT.Cool *resolves* such alias by
looking up the target configuration and connects to the broker running
on the host address indicated by `server_address`, using all the other
connection settings.

</div>

<div class="paragraph">

To get back to the previous example, when a client connects by providing
the alias `mosquitto`, MQTT.Cool will connect to the MQTT broker running
on localhost and listening on port 1883 (`mosquitto.server_address`),
using a connection timeout of 5 seconds (`mosquitto.connection_timeout`)
and a keep alive interval of 10 seconds (`mosquitto.keep_alive`).

</div>

<div class="sect3">

#### 2.1.1. The Hook Variant {#static_lookup_hook}

<div class="paragraph">

The Static Lookup may also be extended by a plugged Hook, which may be
programmed to resolve the provided connection alias, as will be further
detailed in [Section 4.2.5.1, “Providing Broker
Configuration”](#hook_broker_configuration): when no configurations
exist in `mqtt_master_connector_conf.xml`, MQTT.Cool will ask the Hook
to supply a valid one.

</div>

</div>

<div class="sect3">

#### 2.1.2. Client Side Settings {#_client_side_settings}

<div class="paragraph">

The clients have the opportunity to customize the following connection
settings, which will override the ones defined on the server side:

</div>

<div class="ulist">

-   username

-   password

-   Will Message and related settings

</div>

<div class="paragraph">

The Clean Session flag is **always** provided by clients.

</div>

</div>

<div class="sect3">

#### 2.1.3. Final Considerations {#_final_considerations}

<div class="paragraph">

As you have seen so far, the Static Lookup offers several major
benefits:

</div>

<div class="ulist">

-   **Reduced complexity**: the clients do not have to deal with any
    MQTT connection settings (though they could provide specific
    overriding values).

-   **Increased security**: URLs and ports are never specified.

-   **Access restriction**: only configured MQTT brokers can be reached.

-   **Increased flexibility**: MQTT broker host addresses and other
    parameters can change without affecting the client side deployed
    code.

-   **Multiple settings**: several configurations could be defined for
    the same MQTT broker in order to meet different requirements coming
    from different kinds of client applications.

</div>

</div>

</div>

<div class="sect2">

### 2.2. Dynamic Lookup {#dynamic_lookup}

<div class="paragraph">

The *Dynamic Lookup* is triggered when the clients connect to an MQTT
broker whose connection parameters have not been statically configured
on the server side, by supplying an explicit *URI* of the target host.

</div>

<div class="paragraph">

The provided URI has to be expressed in one of the following forms:

</div>

<div class="ulist">

-   `mqtt://<mqtt_broker_address>:<mqtt_broker_port>`

-   `tcp://<mqtt_broker_address>:<mqtt_broker_port>`

</div>

<div class="paragraph">

MQTT.Cool will bypass any provided static configuration and will connect
to the MQTT broker running on the host at the supplied address; in
addition, the following connection settings will be used:

</div>

<div class="ulist">

-   Connection timeout: 5 seconds

-   Keep alive interval: 30 seconds

</div>

<div class="sect3">

#### 2.2.1. Client Side Settings {#_client_side_settings_2}

<div class="paragraph">

As for the Static Lookup, the clients may specify other connection
settings:

</div>

<div class="ulist">

-   username

-   password

-   Will Message along with relative settings

</div>

<div class="paragraph">

Once again, the Clean Session flag is provided only on the client side.

</div>

</div>

<div class="sect3">

#### 2.2.2. Final Considerations {#_final_considerations_2}

<div class="paragraph">

By employing the Dynamic Lookup, you will lose all the benefits
described for the Static Lookup; however, some use cases could take
advantage of this feature, for example:

</div>

<div class="ulist">

-   To prototype a client application for which a backend infrastructure
    has not been consolidated yet.

-   For client test tools which let users decide the MQTT broker to
    connect to.

-   To gather and compare performance metrics between an MQTT broker
    running inside your own infrastructure (e.g, data center, cloud,
    etc…​) and an external one.

</div>

</div>

</div>

</div>

</div>

<div class="sect1">

3. Client Application Development {#_client_application_development}
---------------------------------

<div class="sectionbody">

<div class="paragraph">

In this chapter, we will give a general overview on how to create client
applications that interact with any MQTT broker through the mediation of
MQTT.Cool.

</div>

<div class="sect2">

### 3.1. The SDKs {#_the_sdks}

<div class="paragraph">

You can use two different SDKs to develop JavaScript client
applications:

</div>

<div class="ulist">

-   **SDK for Web Clients**, for development of clients running inside
    the web browser.

-   **SDK for Node.js Clients**, for development of clients running on
    the Node.js runtime.

</div>

<div class="paragraph">

The SDKs provide a unified API that has been designed to be formally
equivalent to the *Eclipse Paho JavaScript Client* as much as possible,
thus allowing you to seamlessly migrate existing client applications.

</div>

<div class="paragraph">

More SDKs for different client-side technologies (including Android and
iOS) are currently under development and will be available soon.

</div>

<div class="sect3">

#### 3.1.1. Deployment Architecture {#_deployment_architecture}

<div class="paragraph">

Before starting to develop your web application, you should evaluate the
most appropriate deployment architecture to employ.

</div>

<div class="paragraph">

Even tough MQTT.Cool comes with an internal web server that can serve
static content, normally this solution should be taken into
consideration only for the purpose of test and demo, as it allows to
easily run out-of-the-box prototypes and samples.

</div>

<div class="paragraph">

On the contrary, for production scenarios it is highly recommended to
deploy an architecture similar to the following:

</div>

<div class="imageblock" style="text-align: right">

<div class="content">

![web
deployment](data:image/svg+xml;base64,PCFET0NUWVBFIHN2ZyBQVUJMSUMgIi0vL1czQy8vRFREIFNWRyAxLjEvL0VOIiAiaHR0cDovL3d3dy53My5vcmcvR3JhcGhpY3MvU1ZHLzEuMS9EVEQvc3ZnMTEuZHRkIj4KPHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHhtbG5zOnhsaW5rPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hsaW5rIiB3aWR0aD0iMTAyMXB4IiBoZWlnaHQ9IjQxMXB4IiB2ZXJzaW9uPSIxLjEiIHN0eWxlPSJiYWNrZ3JvdW5kLWNvbG9yOiByZ2IoMjU1LCAyNTUsIDI1NSk7Ij48ZGVmcy8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoMC41LDAuNSkiPjxyZWN0IHg9IjAiIHk9IjAiIHdpZHRoPSIxMDIwIiBoZWlnaHQ9IjQxMCIgZmlsbD0iI2ZmZmZmZiIgc3Ryb2tlPSJub25lIiBwb2ludGVyLWV2ZW50cz0ibm9uZSIvPjxwYXRoIGQ9Ik0gODc4IDIxNiBMIDg1OCAyMTYgTCA4NTggMTExIEwgNzUyLjk5IDExMSIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjYzA3NTFmIiBzdHJva2Utd2lkdGg9IjIiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9Im5vbmUiLz48cGF0aCBkPSJNIDc0Ni4yNCAxMTEgTCA3NTUuMjQgMTA2LjUgTCA3NTIuOTkgMTExIEwgNzU1LjI0IDExNS41IFoiIGZpbGw9IiNjMDc1MWYiIHN0cm9rZT0iI2MwNzUxZiIgc3Ryb2tlLXdpZHRoPSIyIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJub25lIi8+PHBhdGggZD0iTSA1NzggMjYzIEwgMzE3IDI2MyBMIDMxNyAyNDMuMjQiIGZpbGw9Im5vbmUiIHN0cm9rZT0iI2MwNzUxZiIgc3Ryb2tlLXdpZHRoPSIyIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJub25lIi8+PHBhdGggZD0iTSAzMTcgMjM0LjI0IEwgMzIzIDI0Ni4yNCBMIDMxNyAyNDMuMjQgTCAzMTEgMjQ2LjI0IFoiIGZpbGw9IiNjMDc1MWYiIHN0cm9rZT0iI2MwNzUxZiIgc3Ryb2tlLXdpZHRoPSIyIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJub25lIi8+PGcgZmlsbD0iI0MwNzUxRiIgZm9udC1mYW1pbHk9IkhlbHZldGljYSIgZm9udC13ZWlnaHQ9ImJvbGQiIHRleHQtYW5jaG9yPSJtaWRkbGUiIGZvbnQtc2l6ZT0iMTRweCI+PHRleHQgeD0iNTMxLjUiIHk9IjI0MS41Ij5XZWI8L3RleHQ+PHRleHQgeD0iNTMxLjUiIHk9IjI1OC41Ij5yZXNvdXJjZXM8L3RleHQ+PC9nPjxwYXRoIGQ9Ik0gMjYxLjUgMTI3LjUgQyAyMzEuNSAxMjcuNSAyMjQgMTY1IDI0OCAxNzIuNSBDIDIyNCAxODkgMjUxIDIyNSAyNzAuNSAyMTAgQyAyODQgMjQwIDMyOSAyNDAgMzQ0IDIxMCBDIDM3NCAyMTAgMzc0IDE4MCAzNTUuMjUgMTY1IEMgMzc0IDEzNSAzNDQgMTA1IDMxNy43NSAxMjAgQyAyOTkgOTcuNSAyNjkgOTcuNSAyNjEuNSAxMjcuNSBaIiBmaWxsPSIjZmZmZmZmIiBzdHJva2U9IiMyYTVlNzQiIHN0cm9rZS13aWR0aD0iMiIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0ibm9uZSIvPjxnIGZpbGw9IiMyQTVFNzQiIGZvbnQtZmFtaWx5PSJIZWx2ZXRpY2EiIHRleHQtYW5jaG9yPSJtaWRkbGUiIGZvbnQtc2l6ZT0iMThweCI+PHRleHQgeD0iMjk4IiB5PSIxNzEiPkludGVybmV0PC90ZXh0PjwvZz48cmVjdCB4PSI4NzgiIHk9IjQ4IiB3aWR0aD0iMTAwIiBoZWlnaHQ9IjgwIiByeD0iMTIiIHJ5PSIxMiIgZmlsbD0iI2MwNzUxZiIgc3Ryb2tlPSJub25lIiBwb2ludGVyLWV2ZW50cz0ibm9uZSIvPjxnIGZpbGw9IiNGRkZGRkYiIGZvbnQtZmFtaWx5PSJIZWx2ZXRpY2EiIHRleHQtYW5jaG9yPSJtaWRkbGUiIGZvbnQtc2l6ZT0iMTdweCI+PHRleHQgeD0iOTI3LjUiIHk9Ijg0Ij5NUVRUwqA8L3RleHQ+PHRleHQgeD0iOTI3LjUiIHk9IjEwNCI+QnJva2VyPC90ZXh0PjwvZz48cGF0aCBkPSJNIDE4NC4zNyAxNzMgTCAyMzUuNjMgMTczIiBmaWxsPSJub25lIiBzdHJva2U9IiMyYTVlNzQiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9Im5vbmUiLz48cGF0aCBkPSJNIDE3OS4xMiAxNzMgTCAxODYuMTIgMTY5LjUgTCAxODQuMzcgMTczIEwgMTg2LjEyIDE3Ni41IFoiIGZpbGw9IiMyYTVlNzQiIHN0cm9rZT0iIzJhNWU3NCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0ibm9uZSIvPjxwYXRoIGQ9Ik0gMjQwLjg4IDE3MyBMIDIzMy44OCAxNzYuNSBMIDIzNS42MyAxNzMgTCAyMzMuODggMTY5LjUgWiIgZmlsbD0iIzJhNWU3NCIgc3Ryb2tlPSIjMmE1ZTc0IiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJub25lIi8+PHJlY3QgeD0iNTQ4IiB5PSIzOSIgd2lkdGg9IjE5NiIgaGVpZ2h0PSI5NiIgcng9IjE0LjQiIHJ5PSIxNC40IiBmaWxsPSIjMmE1ZTc0IiBzdHJva2U9Im5vbmUiIHBvaW50ZXItZXZlbnRzPSJub25lIi8+PGcgZmlsbD0iI0ZGRkZGRiIgZm9udC1mYW1pbHk9IkhlbHZldGljYSIgdGV4dC1hbmNob3I9Im1pZGRsZSIgZm9udC1zaXplPSIxN3B4Ij48dGV4dCB4PSI2NDUuNSIgeT0iOTMiPk1RVFQuQ29vbDwvdGV4dD48L2c+PHJlY3QgeD0iNTc4IiB5PSIyMTUiIHdpZHRoPSIxMTAiIGhlaWdodD0iOTYiIHJ4PSIxNC40IiByeT0iMTQuNCIgZmlsbD0iI2MwNzUxZiIgc3Ryb2tlPSJub25lIiBwb2ludGVyLWV2ZW50cz0ibm9uZSIvPjxnIGZpbGw9IiNGRkZGRkYiIGZvbnQtZmFtaWx5PSJIZWx2ZXRpY2EiIHRleHQtYW5jaG9yPSJtaWRkbGUiIGZvbnQtc2l6ZT0iMTdweCI+PHRleHQgeD0iNjMyLjUiIHk9IjI2OSI+V2ViIFNlcnZlcjwvdGV4dD48L2c+PHBhdGggZD0iTSA2MzAgMTY5IEwgNjE0IDE2OSBMIDYxNCA1MjQgTCA2MzAgNTI0IiBmaWxsPSJub25lIiBzdHJva2U9IiM3NDUyMmEiIHN0cm9rZS13aWR0aD0iMiIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiB0cmFuc2Zvcm09InJvdGF0ZSgtOTAsNjE0LDM0Ni41KSIgcG9pbnRlci1ldmVudHM9Im5vbmUiLz48cGF0aCBkPSJNIDU5OCAzNDYuNSBMIDYxNCAzNDYuNSIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjNzQ1MjJhIiBzdHJva2Utd2lkdGg9IjIiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgdHJhbnNmb3JtPSJyb3RhdGUoLTkwLDYxNCwzNDYuNSkiIHBvaW50ZXItZXZlbnRzPSJub25lIi8+PGcgZmlsbD0iIzc0NTIyQSIgZm9udC1mYW1pbHk9IkhlbHZldGljYSIgdGV4dC1hbmNob3I9Im1pZGRsZSIgZm9udC1zaXplPSIxNHB4Ij48dGV4dCB4PSI2MTMuNSIgeT0iMzc5LjUiPkRNWjwvdGV4dD48L2c+PHJlY3QgeD0iODc4IiB5PSIxOTIiIHdpZHRoPSIxMTAiIGhlaWdodD0iOTYiIHJ4PSIxNC40IiByeT0iMTQuNCIgZmlsbD0iI2MwNzUxZiIgc3Ryb2tlPSJub25lIiBwb2ludGVyLWV2ZW50cz0ibm9uZSIvPjxnIGZpbGw9IiNGRkZGRkYiIGZvbnQtZmFtaWx5PSJIZWx2ZXRpY2EiIHRleHQtYW5jaG9yPSJtaWRkbGUiIGZvbnQtc2l6ZT0iMTdweCI+PHRleHQgeD0iOTMyLjUiIHk9IjIzNiI+T3RoZXI8L3RleHQ+PHRleHQgeD0iOTMyLjUiIHk9IjI1NiI+QmFja2VuZHM8L3RleHQ+PC9nPjxwYXRoIGQ9Ik0gNjk5LjI0IDI2My4wNiBMIDg3OCAyNjQiIGZpbGw9Im5vbmUiIHN0cm9rZT0iI2MwNzUxZiIgc3Ryb2tlLXdpZHRoPSIyIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJub25lIi8+PHBhdGggZD0iTSA2OTAuMjQgMjYzLjAxIEwgNzAyLjI3IDI1Ny4wOCBMIDY5OS4yNCAyNjMuMDYgTCA3MDIuMiAyNjkuMDcgWiIgZmlsbD0iI2MwNzUxZiIgc3Ryb2tlPSIjYzA3NTFmIiBzdHJva2Utd2lkdGg9IjIiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9Im5vbmUiLz48cGF0aCBkPSJNIDc1Mi45OSA4Ny4wNSBMIDg2OS4wMSA4Ny42OCIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjYzA3NTFmIiBzdHJva2Utd2lkdGg9IjIiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9Im5vbmUiLz48cGF0aCBkPSJNIDc0Ni4yNCA4Ny4wMSBMIDc1NS4yNiA4Mi41NiBMIDc1Mi45OSA4Ny4wNSBMIDc1NS4yMSA5MS41NiBaIiBmaWxsPSIjYzA3NTFmIiBzdHJva2U9IiNjMDc1MWYiIHN0cm9rZS13aWR0aD0iMiIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0ibm9uZSIvPjxwYXRoIGQ9Ik0gODc1Ljc2IDg3LjcyIEwgODY2Ljc0IDkyLjE3IEwgODY5LjAxIDg3LjY4IEwgODY2Ljc5IDgzLjE3IFoiIGZpbGw9IiNjMDc1MWYiIHN0cm9rZT0iI2MwNzUxZiIgc3Ryb2tlLXdpZHRoPSIyIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJub25lIi8+PHJlY3QgeD0iNjU4IiB5PSIxNzQiIHdpZHRoPSIyNzAiIGhlaWdodD0iMjEiIGZpbGw9IiM3NDUyMmEiIHN0cm9rZT0ibm9uZSIgdHJhbnNmb3JtPSJyb3RhdGUoLTkwLDc5MywxODQuNSkiIHBvaW50ZXItZXZlbnRzPSJub25lIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoNzYxLjUsMTc4LjUpcm90YXRlKC05MCwzMSw2KSI+PHN3aXRjaD48Zm9yZWlnbk9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6dmlzaWJsZTsiIHBvaW50ZXItZXZlbnRzPSJhbGwiIHdpZHRoPSI2MiIgaGVpZ2h0PSIxMiIgcmVxdWlyZWRGZWF0dXJlcz0iaHR0cDovL3d3dy53My5vcmcvVFIvU1ZHMTEvZmVhdHVyZSNFeHRlbnNpYmlsaXR5Ij48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDEycHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiByZ2IoMjU1LCAyNTUsIDI1NSk7IGxpbmUtaGVpZ2h0OiAxLjI7IHZlcnRpY2FsLWFsaWduOiB0b3A7IHdpZHRoOiA2MnB4OyB3aGl0ZS1zcGFjZTogbm93cmFwOyB3b3JkLXdyYXA6IG5vcm1hbDsgZm9udC13ZWlnaHQ6IGJvbGQ7IHRleHQtYWxpZ246IGNlbnRlcjsiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OmlubGluZS1ibG9jazt0ZXh0LWFsaWduOmluaGVyaXQ7dGV4dC1kZWNvcmF0aW9uOmluaGVyaXQ7Ij5GSVJFV0FMTDwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48dGV4dCB4PSIzMSIgeT0iMTIiIGZpbGw9IiNGRkZGRkYiIHRleHQtYW5jaG9yPSJtaWRkbGUiIGZvbnQtc2l6ZT0iMTJweCIgZm9udC1mYW1pbHk9IkhlbHZldGljYSIgZm9udC13ZWlnaHQ9ImJvbGQiPkZJUkVXQUxMPC90ZXh0Pjwvc3dpdGNoPjwvZz48cGF0aCBkPSJNIDUzNi43NiA4NyBMIDMxNyA4NyBMIDMxNy4yIDEwNC43NiIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMmE1ZTc0IiBzdHJva2Utd2lkdGg9IjIiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9Im5vbmUiLz48cGF0aCBkPSJNIDU0NS43NiA4NyBMIDUzMy43NiA5MyBMIDUzNi43NiA4NyBMIDUzMy43NiA4MSBaIiBmaWxsPSIjMmE1ZTc0IiBzdHJva2U9IiMyYTVlNzQiIHN0cm9rZS13aWR0aD0iMiIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0ibm9uZSIvPjxwYXRoIGQ9Ik0gMzE3LjMxIDExMy43NiBMIDMxMS4xNyAxMDEuODMgTCAzMTcuMiAxMDQuNzYgTCAzMjMuMTcgMTAxLjcgWiIgZmlsbD0iIzJhNWU3NCIgc3Ryb2tlPSIjMmE1ZTc0IiBzdHJva2Utd2lkdGg9IjIiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9Im5vbmUiLz48ZyBmaWxsPSIjMkE1RTc0IiBmb250LWZhbWlseT0iSGVsdmV0aWNhIiBmb250LXdlaWdodD0iYm9sZCIgdGV4dC1hbmNob3I9Im1pZGRsZSIgZm9udC1zaXplPSIxNHB4Ij48dGV4dCB4PSI1MDYiIHk9IjEwNSI+UmVhbC10aW1lPC90ZXh0Pjx0ZXh0IHg9IjUwNiIgeT0iMTIyIj5kYXRhPC90ZXh0PjwvZz48cmVjdCB4PSIzMDAiIHk9IjE3MyIgd2lkdGg9IjI3MCIgaGVpZ2h0PSIyMSIgZmlsbD0iIzc0NTIyYSIgc3Ryb2tlPSJub25lIiB0cmFuc2Zvcm09InJvdGF0ZSgtOTAsNDM1LDE4My41KSIgcG9pbnRlci1ldmVudHM9Im5vbmUiLz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSg0MDMuNSwxNzcuNSlyb3RhdGUoLTkwLDMxLDYpIj48c3dpdGNoPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzp2aXNpYmxlOyIgcG9pbnRlci1ldmVudHM9ImFsbCIgd2lkdGg9IjYyIiBoZWlnaHQ9IjEyIiByZXF1aXJlZEZlYXR1cmVzPSJodHRwOi8vd3d3LnczLm9yZy9UUi9TVkcxMS9mZWF0dXJlI0V4dGVuc2liaWxpdHkiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTJweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6IHJnYigyNTUsIDI1NSwgMjU1KTsgbGluZS1oZWlnaHQ6IDEuMjsgdmVydGljYWwtYWxpZ246IHRvcDsgd2lkdGg6IDYycHg7IHdoaXRlLXNwYWNlOiBub3dyYXA7IHdvcmQtd3JhcDogbm9ybWFsOyBmb250LXdlaWdodDogYm9sZDsgdGV4dC1hbGlnbjogY2VudGVyOyI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6aW5saW5lLWJsb2NrO3RleHQtYWxpZ246aW5oZXJpdDt0ZXh0LWRlY29yYXRpb246aW5oZXJpdDsiPkZJUkVXQUxMPC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0Pjx0ZXh0IHg9IjMxIiB5PSIxMiIgZmlsbD0iI0ZGRkZGRiIgdGV4dC1hbmNob3I9Im1pZGRsZSIgZm9udC1zaXplPSIxMnB4IiBmb250LWZhbWlseT0iSGVsdmV0aWNhIiBmb250LXdlaWdodD0iYm9sZCI+RklSRVdBTEw8L3RleHQ+PC9zd2l0Y2g+PC9nPjxwYXRoIGQ9Ik0gNjE0IDM2NSBRIDYxNCAzNjUgNjE0IDM2NSIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMmE1ZTc0IiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHN0cm9rZS1kYXNoYXJyYXk9IjEgMSIgcG9pbnRlci1ldmVudHM9Im5vbmUiLz48cGF0aCBkPSJNIDYxNCAzNjUgTCA2MTQgMzY1IEwgNjE0IDM2NSBMIDYxNCAzNjUgWiIgZmlsbD0iIzJhNWU3NCIgc3Ryb2tlPSIjMmE1ZTc0IiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJub25lIi8+PHBhdGggZD0iTSAxNDcgMTQzIFEgMTQ3IDE0MyAxNDcgMTQzIiBmaWxsPSJub25lIiBzdHJva2U9IiMyYTVlNzQiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgc3Ryb2tlLWRhc2hhcnJheT0iMSAxIiBwb2ludGVyLWV2ZW50cz0ibm9uZSIvPjxwYXRoIGQ9Ik0gMTQ3IDE0MyBMIDE0NyAxNDMgTCAxNDcgMTQzIEwgMTQ3IDE0MyBaIiBmaWxsPSIjMmE1ZTc0IiBzdHJva2U9IiMyYTVlNzQiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9Im5vbmUiLz48cmVjdCB4PSIyMCIgeT0iMTQzIiB3aWR0aD0iMTU3IiBoZWlnaHQ9IjYwIiBmaWxsPSIjMzI5NmMwIiBzdHJva2U9Im5vbmUiIHBvaW50ZXItZXZlbnRzPSJub25lIi8+PGcgZmlsbD0iI0ZGRkZGRiIgZm9udC1mYW1pbHk9IkhlbHZldGljYSIgdGV4dC1hbmNob3I9Im1pZGRsZSIgZm9udC1zaXplPSIxNHB4Ij48dGV4dCB4PSI5OCIgeT0iMTY5Ij5XZWIgQnJvd3NlciAvTm9kZS5KUzwvdGV4dD48dGV4dCB4PSI5OCIgeT0iMTg2Ij5DbGllbnQ8L3RleHQ+PC9nPjwvZz48L3N2Zz4=)

</div>

<div class="title">

Figure 5. Web deployment architecture

</div>

</div>

<div class="paragraph">

where an external web server (e.g. Apache, nginx, IIS or any other
server of your choice) is used to supply web resources, whereas
MQTT.Cool is in charge of supporting the end-to-end communication
between clients and the MQTT broker; moreover, both the MQTT.Cool server
and the web server are deployed together in the *DMZ* network, while the
MQTT broker is protected by a second firewall. Of course, both servers
can be clustered for fail-over and load balancing.

</div>

<div class="paragraph">

Let’s explore now how to use the offered SDKs.

</div>

</div>

</div>

<div class="sect2">

### 3.2. SDK for Web Clients {#_sdk_for_web_clients}

<div class="paragraph">

The SDK for Web Clients enables any HTML page to act as an *MQTT
client*, that is, ready to send and receive real-time MQTT messages
to/from any MQTT broker which has been connected to the MQTT.Cool
server.

</div>

<div class="sect3">

#### 3.2.1. Installation {#_installation}

<div class="paragraph">

You have different options to install the JavaScript library for Web
Clients, with or without `npm`:

</div>

<div class="sect4">

##### npm {#_npm}

<div class="paragraph">

The library is available as `npm` package, therefore you can download
and install it through the usual command:

</div>

<div class="listingblock">

<div class="content">

``` {.CodeRay .highlight}
npm install mqtt.cool-web-client
```

</div>

</div>

<div class="paragraph">

This installation method is strongly suggested when you are going to
build web applications that depend on many different JavaScript
libraries. In fact, this way you can leverage tools such as
[Webpack](https://webpack.js.org/) or
[Browserify](http://browserify.org/) to bundle all your modules
together, as recommended by the modern (and *cool*) JavaScript best
practices.

</div>

<div class="paragraph">

Alternatively, you could simply include the downloaded library with a
`<script>` tag by pointing to the installation folder:

</div>

<div class="listingblock">

<div class="content">

``` {.CodeRay .highlight}
<html>
<head>
  <script src="./node_modules/mqtt.cool-web-client/dist/mqtt.cool.js"></script>
  ...
</html>
```

</div>

</div>

<div class="paragraph">

Since including `node_modules` is most likely to be a non-efficient way
to load the library, especially from a production perspective, you may
manually copy the JavaScript file into a more appropriate location under
your project layout (`./js/lib` in the example below):

</div>

<div class="listingblock">

<div class="content">

``` {.CodeRay .highlight}
<html>
<head>
  <script src="./js/lib/mqtt.cool.js"></script>
  ...
</html>
```

</div>

</div>

</div>

<div class="sect4">

##### CDN

<div class="paragraph">

As soon the last version of the library is published to `npm`
repository, it will be immediately available trough
[`unpkg`](https://unpkg.com/#/), which you can point directly in the
`script` tag, as follows:

</div>

<div class="listingblock">

<div class="content">

``` {.CodeRay .highlight}
<html>
<head>
  <script src="https://unpkg.com/mqtt.cool-web-client"></script>
  ...
</html>
```

</div>

</div>

<div class="paragraph">

You don’t have to specify the complete path of the js file, as the
package includes the [browser bundle
field](https://github.com/defunctzombie/package-browser-field-spec).

</div>

<div class="paragraph">

If you want to get a specific library version, then include it in the
url:

</div>

<div class="listingblock">

<div class="content">

``` {.CodeRay .highlight}
<script src="https://unpkg.com/mqtt.cool-web-client@<version>"></script>
```

</div>

</div>

<div class="paragraph">

Have a look at the `unpkg` home page for more detailed information on
other query parameters you may supply.

</div>

<div class="admonitionblock tip">

  ---- -----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  **   Alternatively, since `unpkg` offers a free CDN with no guarantee on the quality of service, you might want to host the library yourself or host it on another CDN. To do this, simply download the library from <https://unpkg.com/mqtt.cool-web-client/dist/mqtt.cool.js>.
  ---- -----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

</div>

</div>

</div>

<div class="sect3">

#### 3.2.2. The UMD Pattern {#_the_umd_pattern}

<div class="paragraph">

The library implements the [UMD](https://github.com/umdjs/umd) pattern,
which means that its API objects can be exposed indifferently as:

</div>

<div class="ulist">

-   [AMD modules](https://github.com/amdjs/amdjs-api/wiki/AMD)

-   [CommonJS](http://www.commonjs.org) modules

-   Global objects

</div>

<div class="paragraph">

This way the same JavaScript file can be used according to your
preferred development style, as will be shown in the following
sub-sections.

</div>

<div class="sect4">

##### Global Objects {#_global_objects}

<div class="paragraph">

When loading the library as illustrated above, the following two objects
will be registered as *global*, attached to the `mqttcool` namespace:

</div>

<div class="ulist">

-   `openSession`: the library entry point, from which other local
    scoped objects can be created to interact with MQTT brokers; such
    function is always required.

-   `Message`: the class to be used for encapsulating MQTT messages;
    normally it is only required when the clients need to send new
    messages.

</div>

<div class="admonitionblock tip">

  ---- -------------------------------------------------------------------------------------------------------------------------------------------------
  **   Starting from [Section 3.4, “The MQTT.Cool Connection Pattern”](#connection_pattern), you will be provided with full details of these concepts.
  ---- -------------------------------------------------------------------------------------------------------------------------------------------------

</div>

<div class="listingblock">

<div class="content">

``` {.CodeRay .highlight}
<script src='mqtt.cool.js'></script>
<script>
  mqttcool.openSession(...);
  ...
  var message = new mqttcool.Message(...);
  ...
</script>
...
```

</div>

</div>

<div class="paragraph">

The library allows you to customize the namespace by using the custom
attribute `data-mqttcool-ns`, as follows:

</div>

<div class="listingblock">

<div class="content">

``` {.CodeRay .highlight}
<script src='mqtt.cool.js' data-mqttcool-ns='my.custom.namespace'></script>
<script>
  my.custom.namespace.openSession(...);
  ...
  var message = new my.custom.namespace.Message(...);
  ...
</script>
...
```

</div>

</div>

<div class="paragraph">

Finally, if you are an *old school* guy, you might decide to remove the
namespace at all, by setting `data-mqttcool-ns` to empty string:

</div>

<div class="listingblock">

<div class="content">

``` {.CodeRay .highlight}
<script src='mqtt.cool.js' data-mqttcool-ns=''></script>
<script>
  openSession(...);
  ...
  var message = Message(...);
  ...
</script>
...
```

</div>

</div>

<div class="paragraph">

Consider that this approach leads to a notable drawback, as you could
easily get name collisions in your application, therefore you must
ensure that no other code or library on your page declares a global
object having the same name as the ones used in the library.

</div>

</div>

<div class="sect4">

##### AMD {#_amd}

<div class="paragraph">

To use the API objects as *AMD*-compliant module, you need an *AMD
Loader*: you might want to use <http://requirejs.org>, as most modern
JavaScript libraries do.

</div>

<div class="paragraph">

The following example shows a basic usage where, after including
`require.js` and mqtt.cool.js, the `require` function is invoked listing
explicitly dependencies on the API objects.

</div>

<div class="listingblock">

<div class="content">

``` {.CodeRay .highlight}
<html>
<head>
  <script src="./js/lib/require.js"></script>
  <script src="./js/lib/mqtt.cool.js"></script>
  ...
  <script>
    require(['mqttcool/openSession', 'mqttcool/Message'], function(openSession, Message) {
      openSession(...);
      ...
    });
  </script>
</head>
...
</html>
```

</div>

</div>

<div class="paragraph">

Also im this case, you may use a different namespace and even remove it,
this time through an explicit custom configuration of `require.js`:

</div>

<div class="listingblock">

<div class="content">

``` {.CodeRay .highlight}
<html>
<head>
  <script src="./js/lib/require.js"></script>
  <script>
    requirejs.config({
      // Provide a configuration object to the internal MQTT.Cool library configurator
      config: {
        'mqttcool': {
          'ns': 'my.namespace'  // Set the 'ns' custom attribute to your namespace (or '' for no namespace)
        }
      }
    })
  </script>
  <script src="./js/lib/mqtt.cool.js"></script>
  <script>
    require(['my.namespace/openSession', 'my.namespace/Message'],
      function(openSession, Message) {
        ...
      }
    );
  </script>
</head>
...
</html>
```

</div>

</div>

</div>

</div>

<div class="sect3">

#### 3.2.3. CommonJS {#_commonjs}

<div class="paragraph">

Even if technically compatible with any CommonJS environment like
Node.js, the library has been expressly designed to work in the context
of a web browser. But don’t worry: as already anticipated, a dedicated
SDK is available!

</div>

</div>

</div>

<div class="sect2">

### 3.3. SDK for Node.js Clients {#_sdk_for_node_js_clients}

<div class="paragraph">

The *SDK for Node.js Clients* allows you to develop and execute MQTT
client applications for Node.js, by using the same API already provided
by the *SDK for Web Clients* (even if a few differences exist, as will
be detailed in the next sections).

</div>

<div class="paragraph">

All you have to do is setup your development environment by installing
the package through `npm`:

</div>

<div class="listingblock">

<div class="content">

``` {.CodeRay .highlight}
npm install mqtt.cool-node-client --save
```

</div>

</div>

<div class="admonitionblock note">

  ---- ----------------------------------------------------------------------------------------------------
  **   The additional `--save` flag will update your `package.json` (if any) while installing the module.
  ---- ----------------------------------------------------------------------------------------------------

</div>

<div class="paragraph">

Then you can start writing your application by loading
`mqtt.cool-node-client`, as follows:

</div>

<div class="listingblock">

<div class="content">

``` {.CodeRay .highlight}
// Access the library
const mqttcool = require('mqtt.cool-node-client');

// Start a connection
mqttcool.openSession(...);
...
// Create a new Message instance
var message = new mqttcool.Message(...);
```

</div>

</div>

<div class="paragraph">

As you can see, by leveraging the semantics of Node.js’s `require()`
function you can load the only two concrete API objects needed to
develop a client application.

</div>

</div>

<div class="sect2">

### 3.4. The MQTT.Cool Connection Pattern {#connection_pattern}

<div class="paragraph">

Any client application needs to perform a few basic operations in order
to establish a communication with an MQTT broker.

</div>

<div class="paragraph">

The main connection pattern is shown in the following code snippet:

</div>

<div class="listingblock">

<div class="content">

``` {.CodeRay .highlight}
mqttcool.openSession('http://my.server.company:8080', { (1)

  onConnectionSuccess: function(mqttCoolSession) { (2)

    var mqttClient = mqttCoolSession.createClient('mybroker', 'myclientid'); (3)

    mqttClient.connect(); (4)
  }

});
...
```

</div>

</div>

<div class="colist arabic">

  --------- ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  ****1**   Open a new session against the MQTT.Cool server running at the specified address.
  ****2**   Upon successful connection, the `onConnectionSuccess` callback function is invoked.
  ****3**   Through the `mqttCoolSession` parameter (which implements the [`MQTTCoolSession`](http://www.lightstreamer.com/api/mqtt.cool-web-client/latest/MQTTCoolSession.html) interface), create a new [`MqttClient`](http://www.lightstreamer.com/api/mqtt.cool-web-client/latest/MqttClient.html) instance that is configured to connect to the MQTT broker aliased by *mybroker*, using *myclientid* as client identifier.
  ****4**   Connect to the MQTT broker.
  --------- ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

</div>

<div class="paragraph">

Let’s highlight some important variants of the main pattern:

</div>

<div class="ulist">

-   You can open a session to the MQTT.Cool server also specifying
    username and password, which will be checked by the plugged Hook, if
    any (as will be detailed in [Section 4.2.4, “Authorizing Session
    Opening”](#hook_authorizing_session)). For example:

    <div class="listingblock">

    <div class="content">

    ``` {.CodeRay .highlight}
    mqttcool.openSession('http://my.cool.server.company:8080', 'my_cool_user', 'my_cool_password', {
      ...
      }
    );
    ```

    </div>

    </div>

    <div class="admonitionblock tip">

      ---- -----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
      **   See the [`openSession`](http://www.lightstreamer.com/api/mqtt.cool-web-client/latest/global.html#openSession) API reference for a complete description of all allowed invocation forms.
      ---- -----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

    </div>

-   As already mentioned in [Section 2.1, “Static
    Lookup”](#static_lookup), normally you will use an alias to
    statically lookup the connection settings relative to the MQTT
    broker to connect to; but you could also lean on the Dynamic Lookup
    (see [Section 2.2, “Dynamic Lookup”](#dynamic_lookup)) to bypass any
    static configuration and connect to the supplied URI, as in the
    following example:

    <div class="listingblock">

    <div class="content">

    ``` {.CodeRay .highlight}
    ...
    var mqttClient = mqttCoolSession.createClient('tcp://other.mqtt.broker:1883', 'myclientid');
    ...
    ```

    </div>

    </div>

-   An `MqttClient` instance could also be created without a client
    identifier, thus enabling a *shared connection* (which will be
    discussed later), as follows:

    <div class="listingblock">

    <div class="content">

    ``` {.CodeRay .highlight}
    ...
    var mqttClient = mqttCoolSession.createClient('tcp://other.mqtt.broker:1883');
    ...
    ```

    </div>

    </div>

-   You could provide a set of connection options to be used for
    connecting to the target MQTT broker:

    <div class="listingblock">

    <div class="content">

    ``` {.CodeRay .highlight}
    var connectOptions = { ... };
    mqttClient.connect(connectOptions);
    ```

    </div>

    </div>

</div>

</div>

<div class="sect2">

### 3.5. The MQTTCoolSession Interface {#session_interface}

<div class="paragraph">

As you have seen so far, a fresh `MQTTCoolSession` instance is provided
through the `onConnectionSuccess` callback function once a new
connection to MQTT.Cool has been successfully established.

</div>

<div class="paragraph">

Such connection, called *MQTT.Cool connection*, is managed by
`MQTTCoolSession` to handle the bidirectional communications between
every `MqttClient` instance it can create and the target MQTT.Cool
server process, in order to support the end-to-end communications with
MQTT brokers. Every `MQTTCoolSession` object is bound to the MQTT.Cool
connection established through an `opnSession` call.

</div>

<div class="paragraph">

Multiple invocations of `openSession` with the same server address will
result in providing distinct `MQTTCoolSession` instances, which will
handle their own underlying connections independently of each other,
thus letting you manage as many separate sessions as you want.

</div>

<div class="paragraph">

In addition to the `onConnectionSuccess` callback, other handlers are
provided to be notified of events related to the life cycle of an
`MQTTCoolSession` object. They are defined through the
[`MQTTCoolListener`](http://www.lightstreamer.com/api/mqtt.cool-web-client/latest/MQTTCoolListener.html)
interface, which is formally required as the last argument to be passed
to the `openSession` function.

</div>

<div class="paragraph">

A complete handling of all expected callbacks involves a slight
extension of the main connection pattern:

</div>

<div id="main_connection_pattern_ext" class="listingblock">

<div class="content">

``` {.CodeRay .highlight}
mqttcool.openSession(..., {

  onLsClient: function(lsClient) { ... },

  onConnectionSuccess: function(mqttCoolSession) { ... },

  onConnectionFailure: function(errorType, errorCode, errorMessage) { ... }

});
```

</div>

</div>

<div class="paragraph">

where:

</div>

<div class="ulist">

-   [`onLsClient`](http://www.lightstreamer.com/api/mqtt.cool-web-client/latest/MQTTCoolListener.html#onLsClient)
    is the first fired event when the embedded *Lightstreamer Session*
    is initialized, but before actually opening the connection to
    MQTT.Cool (see [Appendix B, *Access the Lightstreamer Client
    API*](#_access_the_lightstreamer_client_api)).

-   [`onConnectionFailure`](http://www.lightstreamer.com/api/mqtt.cool-web-client/latest/MQTTCoolListener.html#onConnectionFailure)
    is invoked if the connection to MQTT.Cool cannot be established and,
    as consequence of this, no `MQTTCoolSession` objects can be
    activated.

</div>

<div class="admonitionblock note">

  ---- ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  **   Connection failures may also include any authorization issue raised by the plugged Hook, as will be discussed in [Section 4.2.4, “Authorizing Session Opening”](#hook_authorizing_session).
  ---- ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

</div>

</div>

<div class="sect2">

### 3.6. The MqttClient Interface {#_the_mqttclient_interface}

<div class="paragraph">

The
[`MqttClient`](http://www.lightstreamer.com/api/mqtt.cool-web-client/latest/MqttClient.html)
interface is used to manage the communication with any MQTT broker
through a set of methods, which let you:

</div>

<div class="ulist">

-   Open a connection.

-   Send messages.

-   Subscribe to topics for receiving messages.

-   Unsubscribe from topics.

-   Manage connection and authorization issues.

-   Disconnect.

</div>

<div class="paragraph">

An instance of `MqttClient` enables an *end-to-end* virtual connection
to the broker as if there was a direct link between the two endpoints.

</div>

<div class="imageblock" style="text-align: center">

<div class="content">

![end to end
connection](data:image/svg+xml;base64,PCFET0NUWVBFIHN2ZyBQVUJMSUMgIi0vL1czQy8vRFREIFNWRyAxLjEvL0VOIiAiaHR0cDovL3d3dy53My5vcmcvR3JhcGhpY3MvU1ZHLzEuMS9EVEQvc3ZnMTEuZHRkIj4KPHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHhtbG5zOnhsaW5rPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hsaW5rIiB3aWR0aD0iOTkxcHgiIGhlaWdodD0iMzUxcHgiIHZlcnNpb249IjEuMSIgc3R5bGU9ImJhY2tncm91bmQtY29sb3I6IHJnYigyNTUsIDI1NSwgMjU1KTsiPjxkZWZzLz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgwLjUsMC41KSI+PHJlY3QgeD0iMCIgeT0iMCIgd2lkdGg9Ijk5MCIgaGVpZ2h0PSIzNTAiIGZpbGw9IiNmZmZmZmYiIHN0cm9rZT0ibm9uZSIgcG9pbnRlci1ldmVudHM9Im5vbmUiLz48cGF0aCBkPSJNIDYwNS41IDE0MSBMIDYwNS41IDE1MS41IEwgNTg2LjUgMTM2IEwgNjA1LjUgMTIwLjUgTCA2MDUuNSAxMzEgTCA3NDYuNSAxMzEgTCA3NDYuNSAxMjAuNSBMIDc2NS41IDEzNiBMIDc0Ni41IDE1MS41IEwgNzQ2LjUgMTQxIFoiIGZpbGw9IiNjMDc1MWYiIHN0cm9rZT0ibm9uZSIgcG9pbnRlci1ldmVudHM9Im5vbmUiLz48ZyBmaWxsPSIjQzA3NTFGIiBmb250LWZhbWlseT0iSGVsdmV0aWNhIiB0ZXh0LWFuY2hvcj0ibWlkZGxlIiBmb250LXNpemU9IjE1cHgiPjx0ZXh0IHg9IjY3My41IiB5PSIxMDYiPkJyb2tlcsKgPC90ZXh0Pjx0ZXh0IHg9IjY3My41IiB5PSIxMjQiPmNvbm5lY3Rpb248L3RleHQ+PC9nPjxyZWN0IHg9IjM3OSIgeT0iMzEiIHdpZHRoPSIyMDciIGhlaWdodD0iMjEwIiByeD0iMzEuMDUiIHJ5PSIzMS4wNSIgZmlsbD0iIzJhNWU3NCIgc3Ryb2tlPSJub25lIiBwb2ludGVyLWV2ZW50cz0ibm9uZSIvPjxnIGZpbGw9IiNGRkZGRkYiIGZvbnQtZmFtaWx5PSJIZWx2ZXRpY2EiIHRleHQtYW5jaG9yPSJtaWRkbGUiIGZvbnQtc2l6ZT0iMTdweCI+PHRleHQgeD0iNDgyIiB5PSIxNDIiPk1RVFQuQ29vbDwvdGV4dD48L2c+PHJlY3QgeD0iNzY2IiB5PSI3MSIgd2lkdGg9IjEzOSIgaGVpZ2h0PSIxMzAiIHJ4PSIxOS41IiByeT0iMTkuNSIgZmlsbD0iI2MwNzUxZiIgc3Ryb2tlPSJub25lIiBwb2ludGVyLWV2ZW50cz0ibm9uZSIvPjxnIGZpbGw9IiNGRkZGRkYiIGZvbnQtZmFtaWx5PSJIZWx2ZXRpY2EiIHRleHQtYW5jaG9yPSJtaWRkbGUiIGZvbnQtc2l6ZT0iMTRweCI+PHRleHQgeD0iODM1IiB5PSIxNDAuNSI+TVFUVCBCcm9rZXI8L3RleHQ+PC9nPjxwYXRoIGQ9Ik0gMTc5LjUyIDE0MS45MSBMIDE3OS41NyAxNTIuNDEgTCAxNjAuNSAxMzcgTCAxNzkuNDMgMTIxLjQxIEwgMTc5LjQ4IDEzMS45MSBMIDM1OS40OCAxMzEuMDkgTCAzNTkuNDMgMTIwLjU5IEwgMzc4LjUgMTM2IEwgMzU5LjU3IDE1MS41OSBMIDM1OS41MiAxNDEuMDkgWiIgZmlsbD0iIzJhNWU3NCIgc3Ryb2tlPSJub25lIiBwb2ludGVyLWV2ZW50cz0ibm9uZSIvPjxnIGZpbGw9IiMyQTVFNzQiIGZvbnQtZmFtaWx5PSJIZWx2ZXRpY2EiIHRleHQtYW5jaG9yPSJtaWRkbGUiIGZvbnQtc2l6ZT0iMTVweCI+PHRleHQgeD0iMjY4LjQzIiB5PSI4NC41Ij5NUVRUIGNoYW5uZWw8L3RleHQ+PHRleHQgeD0iMjY4LjQzIiB5PSIxMDIuNSI+b3ZlcsKgPC90ZXh0Pjx0ZXh0IHg9IjI2OC40MyIgeT0iMTIwLjUiPk1RVFQuQ29vbCBjb25uZWN0aW9uPC90ZXh0PjwvZz48ZyBmaWxsPSIjNTlBMkMwIiBmb250LWZhbWlseT0iSGVsdmV0aWNhIiBmb250LXdlaWdodD0iYm9sZCIgZm9udC1zdHlsZT0iaXRhbGljIiB0ZXh0LWFuY2hvcj0ibWlkZGxlIiBmb250LXNpemU9IjE3cHgiPjx0ZXh0IHg9IjQ3NC41IiB5PSIyOTIiPkVuZC10by1lbmQgVmlydHVhbCBjb25uZWN0aW9uPC90ZXh0PjwvZz48cmVjdCB4PSI1MCIgeT0iODciIHdpZHRoPSIxMTAiIGhlaWdodD0iOTkiIGZpbGw9IiMzMjk2YzAiIHN0cm9rZT0ibm9uZSIgcG9pbnRlci1ldmVudHM9Im5vbmUiLz48ZyBmaWxsPSIjRkZGRkZGIiBmb250LWZhbWlseT0iSGVsdmV0aWNhIiB0ZXh0LWFuY2hvcj0ibWlkZGxlIiBmb250LXNpemU9IjE0cHgiPjx0ZXh0IHg9IjEwNC41IiB5PSIxNDEiPk1xdHRDbGllbnQ8L3RleHQ+PC9nPjxyZWN0IHg9IjQyMiIgeT0iMzE1IiB3aWR0aD0iMTIwIiBoZWlnaHQ9IjE4IiBmaWxsPSIjZmZmZmZmIiBzdHJva2U9IiNmZmZmZmYiIHBvaW50ZXItZXZlbnRzPSJub25lIi8+PHBhdGggZD0iTSA5OS41IDIyMSBMIDg4LjUgMjIxIEwgMTA1IDIwMSBMIDEyMS41IDIyMSBMIDExMC41IDIyMSBMIDExMC41IDMwNC41IEwgODI1LjUgMzA0LjUgTCA4MjUuNSAyMzEgTCA4MTQuNSAyMzEgTCA4MzEgMjExIEwgODQ3LjUgMjMxIEwgODM2LjUgMjMxIEwgODM2LjUgMzA0LjUgUSA4MzYuNSAzMTUuNSA4MjUuNSAzMTUuNSBMIDExMC41IDMxNS41IFEgOTkuNSAzMTUuNSA5OS41IDMwNC41IFoiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzU5YTJjMCIgc3Ryb2tlLXdpZHRoPSIyIiBzdHJva2UtbGluZWpvaW49InJvdW5kIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHN0cm9rZS1kYXNoYXJyYXk9IjYgNiIgcG9pbnRlci1ldmVudHM9Im5vbmUiLz48cGF0aCBkPSJNIDk5LjUgMjIxIEwgODguNSAyMjEgTCAxMDUgMjAxIEwgMTIxLjUgMjIxIEwgMTEwLjUgMjIxIiBmaWxsPSJub25lIiBzdHJva2U9IiM1OWEyYzAiIHN0cm9rZS13aWR0aD0iMiIgc3Ryb2tlLWxpbmVqb2luPSJmbGF0IiBzdHJva2UtbWl0ZXJsaW1pdD0iNCIgc3Ryb2tlLWRhc2hhcnJheT0iNiA2IiBwb2ludGVyLWV2ZW50cz0ibm9uZSIvPjxwYXRoIGQ9Ik0gODI1LjUgMjMxIEwgODE0LjUgMjMxIEwgODMxIDIxMSBMIDg0Ny41IDIzMSBMIDgzNi41IDIzMSIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjNTlhMmMwIiBzdHJva2Utd2lkdGg9IjIiIHN0cm9rZS1saW5lam9pbj0iZmxhdCIgc3Ryb2tlLW1pdGVybGltaXQ9IjQiIHN0cm9rZS1kYXNoYXJyYXk9IjYgNiIgcG9pbnRlci1ldmVudHM9Im5vbmUiLz48L2c+PC9zdmc+)

</div>

<div class="title">

Figure 6. End-to-end virtual connection between MqttClient and MQTT
Broker

</div>

</div>

<div class="paragraph">

As depicted in the above image, an end-to-end virtual connection is made
up of the following two distinct links:

</div>

<div class="olist arabic">

1.  **MQTT channel**, which is the logical channel established over the
    physical MQTT.Cool connection, between `MqttClient` and the
    MQTT.Cool server.

2.  **broker connection**, which is the physical MQTT connection between
    the MQTT.Cool server and the MQTT broker

</div>

<div class="paragraph">

In an end-to-end connection, MQTT.Cool takes the role of a real MQTT
server proxy, as it acts as an intermediary for the MQTT Control Packets
wrapped into *MQTT.Cool Protocol* messages and transported over the MQTT
channel, as well as for the MQTT Control Packets transported *as is*
over the broker connection.

</div>

<div class="sect3">

#### 3.6.1. Multiplexed MQTT Channels {#_multiplexed_mqtt_channels}

<div class="paragraph">

The client library transparently implements *multiplexed* MQTT channels,
as all the `MqttClient` instances created from the same
`MQTTCoolSession` object establish a new channel over the same MQTT.Cool
connection.

</div>

<div class="paragraph">

Though they are combined into a common physical connection, multiplexed
channels enable separate and isolated end-to-end communications, thus
allowing you to:

</div>

<div class="olist arabic">

1.  Reduce the overhead due to connection setup.

2.  Optimize usage of physical connections.

</div>

<div class="paragraph">

By leveraging multiplexed channels, you can make `MqttClient` instances
connect to single or multiple brokers. The following picture shows an
example where three `MttClient` instances are establishing independent
channels to set up their own end-to-end connection to the target MQTT
broker.

</div>

<div class="imageblock" style="text-align: center">

<div class="content">

![multiplexed](data:image/svg+xml;base64,PCFET0NUWVBFIHN2ZyBQVUJMSUMgIi0vL1czQy8vRFREIFNWRyAxLjEvL0VOIiAiaHR0cDovL3d3dy53My5vcmcvR3JhcGhpY3MvU1ZHLzEuMS9EVEQvc3ZnMTEuZHRkIj4KPHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHhtbG5zOnhsaW5rPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hsaW5rIiB3aWR0aD0iMTA1MXB4IiBoZWlnaHQ9IjM2MXB4IiB2ZXJzaW9uPSIxLjEiIHN0eWxlPSJiYWNrZ3JvdW5kLWNvbG9yOiByZ2IoMjU1LCAyNTUsIDI1NSk7Ij48ZGVmcy8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoMC41LDAuNSkiPjxyZWN0IHg9IjAiIHk9IjAiIHdpZHRoPSIxMDUwIiBoZWlnaHQ9IjM2MCIgZmlsbD0iI2ZmZmZmZiIgc3Ryb2tlPSJub25lIiBwb2ludGVyLWV2ZW50cz0ibm9uZSIvPjxwYXRoIGQ9Ik0gMjI2LjY1IDExOS43NSBMIDQ5My4zNSAxMTkuNzUgTCA0OTMuMzUgMTA0IEwgNTQwIDE3Mi41IEwgNDkzLjM1IDI0MSBMIDQ5My4zNSAyMjUuMjUgTCAyMjYuNjUgMjI1LjI1IEwgMjI2LjY1IDI0MSBMIDE4MCAxNzIuNSBMIDIyNi42NSAxMDQgWiIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMmE1ZTc0IiBzdHJva2Utd2lkdGg9IjIiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9Im5vbmUiLz48ZyBmaWxsPSIjMkE1RTc0IiBmb250LWZhbWlseT0iSGVsdmV0aWNhIiB0ZXh0LWFuY2hvcj0ibWlkZGxlIiBmb250LXNpemU9IjE2cHgiPjx0ZXh0IHg9IjM1OSIgeT0iMjE2LjUiPk1RVFQuQ29vbCBjb25uZWN0aW9uPC90ZXh0PjwvZz48cmVjdCB4PSIxMCIgeT0iMzciIHdpZHRoPSIxNzAiIGhlaWdodD0iMjgwIiByeD0iMjUuNSIgcnk9IjI1LjUiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzU5YTJjMCIgcG9pbnRlci1ldmVudHM9Im5vbmUiLz48ZyBmaWxsPSIjNTlBMkMwIiBmb250LWZhbWlseT0iSGVsdmV0aWNhIiBmb250LXdlaWdodD0iYm9sZCIgdGV4dC1hbmNob3I9Im1pZGRsZSIgZm9udC1zaXplPSIxNHB4Ij48dGV4dCB4PSI5NC41IiB5PSIzMDkuNSI+TVFUVENvb2xTZXNzaW9uPC90ZXh0PjwvZz48cmVjdCB4PSI1NDMiIHk9IjY3IiB3aWR0aD0iMjA2IiBoZWlnaHQ9IjIxMCIgcng9IjMwLjkiIHJ5PSIzMC45IiBmaWxsPSIjMmE1ZTc0IiBzdHJva2U9Im5vbmUiIHBvaW50ZXItZXZlbnRzPSJub25lIi8+PGcgZmlsbD0iI0ZGRkZGRiIgZm9udC1mYW1pbHk9IkhlbHZldGljYSIgdGV4dC1hbmNob3I9Im1pZGRsZSIgZm9udC1zaXplPSIxN3B4Ij48dGV4dCB4PSI2NDUuNSIgeT0iMTc4Ij5NUVRULkNvb2w8L3RleHQ+PC9nPjxyZWN0IHg9IjQwIiB5PSIxNDEiIHdpZHRoPSIxMTAiIGhlaWdodD0iNjAiIGZpbGw9IiMzMjk2YzAiIHN0cm9rZT0ibm9uZSIgcG9pbnRlci1ldmVudHM9Im5vbmUiLz48ZyBmaWxsPSIjRkZGRkZGIiBmb250LWZhbWlseT0iSGVsdmV0aWNhIiB0ZXh0LWFuY2hvcj0ibWlkZGxlIiBmb250LXNpemU9IjE0cHgiPjx0ZXh0IHg9Ijk0LjUiIHk9IjE3NS41Ij5NcXR0Q2xpZW50PC90ZXh0PjwvZz48cmVjdCB4PSI0MCIgeT0iNjIiIHdpZHRoPSIxMTAiIGhlaWdodD0iNjUiIGZpbGw9IiMzMjk2YzAiIHN0cm9rZT0ibm9uZSIgcG9pbnRlci1ldmVudHM9Im5vbmUiLz48ZyBmaWxsPSIjRkZGRkZGIiBmb250LWZhbWlseT0iSGVsdmV0aWNhIiB0ZXh0LWFuY2hvcj0ibWlkZGxlIiBmb250LXNpemU9IjE0cHgiPjx0ZXh0IHg9Ijk0LjUiIHk9Ijk5Ij5NcXR0Q2xpZW50PC90ZXh0PjwvZz48cmVjdCB4PSI0MCIgeT0iMjE3IiB3aWR0aD0iMTEwIiBoZWlnaHQ9IjYwIiBmaWxsPSIjMzI5NmMwIiBzdHJva2U9Im5vbmUiIHBvaW50ZXItZXZlbnRzPSJub25lIi8+PGcgZmlsbD0iI0ZGRkZGRiIgZm9udC1mYW1pbHk9IkhlbHZldGljYSIgdGV4dC1hbmNob3I9Im1pZGRsZSIgZm9udC1zaXplPSIxNHB4Ij48dGV4dCB4PSI5NC41IiB5PSIyNTEuNSI+TXF0dENsaWVudDwvdGV4dD48L2c+PHBhdGggZD0iTSAxNjEuMzEgOTcuMjkgTCAxNjEuMzEgMTAzLjM0IEwgMTUwLjUgOTUgTCAxNjEuMzEgODYuNjYgTCAxNjEuMzEgOTIuNzEgTCAyMTcuNzEgOTIuNzEgUSAyMjIuMjkgOTIuNzEgMjIyLjI5IDk3LjI5IEwgMjIyLjI5IDE0NC43MSBMIDUxMS4xNiAxNDQuNzEgTCA1MTEuMTYgMTM5LjgxIEwgNTE5LjUgMTQ3IEwgNTExLjE2IDE1NC4xOSBMIDUxMS4xNiAxNDkuMjkgTCAyMjIuMjkgMTQ5LjI5IFEgMjE3LjcxIDE0OS4yOSAyMTcuNzEgMTQ0LjcxIEwgMjE3LjcxIDk3LjI5IFoiIGZpbGw9IiMyYTVlNzQiIHN0cm9rZT0ibm9uZSIgcG9pbnRlci1ldmVudHM9Im5vbmUiLz48cGF0aCBkPSJNIDE2MS4zMSAyNDkuMjkgTCAxNjEuMzEgMjU1LjM0IEwgMTUwLjUgMjQ3IEwgMTYxLjMxIDIzOC42NiBMIDE2MS4zMSAyNDQuNzEgTCAyMTcuNzEgMjQ0LjcxIEwgMjE3LjcxIDE5OS4yOSBRIDIxNy43MSAxOTQuNzEgMjIyLjI5IDE5NC43MSBMIDUxMS4xNiAxOTQuNzEgTCA1MTEuMTYgMTg5LjgxIEwgNTE5LjUgMTk3IEwgNTExLjE2IDIwNC4xOSBMIDUxMS4xNiAxOTkuMjkgTCAyMjIuMjkgMTk5LjI5IEwgMjIyLjI5IDI0NC43MSBRIDIyMi4yOSAyNDkuMjkgMjE3LjcxIDI0OS4yOSBaIiBmaWxsPSIjMmE1ZTc0IiBzdHJva2U9Im5vbmUiIHBvaW50ZXItZXZlbnRzPSJub25lIi8+PHBhdGggZD0iTSAxNjEuMyAxNzMuMzIgTCAxNjEuMjggMTc5LjM3IEwgMTUwLjUgMTcxIEwgMTYxLjMzIDE2Mi42OSBMIDE2MS4zMSAxNjguNzQgTCA1MTEuMTcgMTY5LjY5IEwgNTExLjE4IDE2NC43OCBMIDUxOS41IDE3MiBMIDUxMS4xNCAxNzkuMTcgTCA1MTEuMTYgMTc0LjI2IFoiIGZpbGw9IiMyYTVlNzQiIHN0cm9rZT0ibm9uZSIgcG9pbnRlci1ldmVudHM9Im5vbmUiLz48cmVjdCB4PSIzNjAiIHk9IjUyIiB3aWR0aD0iMTAwIiBoZWlnaHQ9IjIwIiByeD0iMyIgcnk9IjMiIGZpbGw9Im5vbmUiIHN0cm9rZT0ibm9uZSIgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoMiwzKSIgb3BhY2l0eT0iMC4yNSIvPjxnIGZpbGw9IiMyQTVFNzQiIGZvbnQtZmFtaWx5PSJIZWx2ZXRpY2EiIGZvbnQtd2VpZ2h0PSJib2xkIiB0ZXh0LWFuY2hvcj0ibWlkZGxlIiBmb250LXNpemU9IjEycHgiPjx0ZXh0IHg9IjQwOS41IiB5PSI2NS41Ij5NUVRUIGNoYW5uZWxzPC90ZXh0PjwvZz48cGF0aCBkPSJNIDM4NSA3MiBMIDM1Mi44MiAxMzcuMjkiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzJhNWU3NCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0ibm9uZSIvPjxwYXRoIGQ9Ik0gMzUwLjQ5IDE0MiBMIDM1MC40NSAxMzQuMTcgTCAzNTIuODIgMTM3LjI5IEwgMzU2LjczIDEzNy4yNyBaIiBmaWxsPSIjMmE1ZTc0IiBzdHJva2U9IiMyYTVlNzQiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9Im5vbmUiLz48cGF0aCBkPSJNIDM5NyA3MiBMIDM2Ni4wNSAxNjIuOTciIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzJhNWU3NCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0ibm9uZSIvPjxwYXRoIGQ9Ik0gMzY0LjM2IDE2Ny45NCBMIDM2My4zIDE2MC4xOSBMIDM2Ni4wNSAxNjIuOTcgTCAzNjkuOTMgMTYyLjQ0IFoiIGZpbGw9IiMyYTVlNzQiIHN0cm9rZT0iIzJhNWU3NCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0ibm9uZSIvPjxwYXRoIGQ9Ik0gNDA5LjIyIDcyIEwgNDAwLjQ5IDE4NC42NSIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMmE1ZTc0IiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJub25lIi8+PHBhdGggZD0iTSA0MDAuMDkgMTg5Ljg5IEwgMzk3LjE0IDE4Mi42NCBMIDQwMC40OSAxODQuNjUgTCA0MDQuMTIgMTgzLjE4IFoiIGZpbGw9IiMyYTVlNzQiIHN0cm9rZT0iIzJhNWU3NCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0ibm9uZSIvPjxyZWN0IHg9IjkxMCIgeT0iMTI2IiB3aWR0aD0iMTIwIiBoZWlnaHQ9Ijk1IiByeD0iMTQuMjUiIHJ5PSIxNC4yNSIgZmlsbD0iI2MwNzUxZiIgc3Ryb2tlPSJub25lIiBwb2ludGVyLWV2ZW50cz0ibm9uZSIvPjxnIGZpbGw9IiNGRkZGRkYiIGZvbnQtZmFtaWx5PSJIZWx2ZXRpY2EiIHRleHQtYW5jaG9yPSJtaWRkbGUiIGZvbnQtc2l6ZT0iMTRweCI+PHRleHQgeD0iOTY5LjUiIHk9IjE3OCI+TVFUVCBCcm9rZXI8L3RleHQ+PC9nPjxwYXRoIGQ9Ik0gNzY4LjUgMTc1IEwgNzY4LjUgMTg1LjUgTCA3NDkuNSAxNzAgTCA3NjguNSAxNTQuNSBMIDc2OC41IDE2NSBMIDg5MC41IDE2NSBMIDg5MC41IDE1NC41IEwgOTA5LjUgMTcwIEwgODkwLjUgMTg1LjUgTCA4OTAuNSAxNzUgWiIgZmlsbD0iI2MwNzUxZiIgc3Ryb2tlPSJub25lIiBwb2ludGVyLWV2ZW50cz0ibm9uZSIvPjxnIGZpbGw9IiNDMDc1MUYiIGZvbnQtZmFtaWx5PSJIZWx2ZXRpY2EiIHRleHQtYW5jaG9yPSJtaWRkbGUiIGZvbnQtc2l6ZT0iMTVweCI+PHRleHQgeD0iODI3LjUiIHk9IjE0MCI+QnJva2VywqA8L3RleHQ+PHRleHQgeD0iODI3LjUiIHk9IjE1OCI+Y29ubmVjdGlvbjwvdGV4dD48L2c+PC9nPjwvc3ZnPg==)

</div>

<div class="title">

Figure 7. Multiplexed MQTT channels

</div>

</div>

<div class="paragraph">

Multiplexing is a very efficient way to manage the communications with
the MQTT.Cool server and MQTT brokers. On the other hand, there could be
circumstances where this is not the desired behavior, for example if you
want to avoid that an MQTT.Cool connection outage affects all engaged
MQTT channels.

</div>

<div class="paragraph">

To prevent a channel from getting multiplexed, you have to initiate
every single connection only from `MqttClient` instances each one
generated by separate `MQTTCoolSession` objects, thus enforcing each
MQTT.Cool connection to host a single MQTT channel.

</div>

<div class="paragraph">

Let’s focus now on broker connections: based on the way they are managed
on the server side, an *end-to-end* connection can be of two types,
*dedicated* or *shared*, as will be detailed in the next two sections.

</div>

</div>

<div class="sect3">

#### 3.6.2. Dedicated End-to-End Connection {#dedicated_connection}

<div class="paragraph">

For each `MqttClient` which has been provided with a valid client
identifier at the time of creation through `MQTTCoolSession`, MQTT.Cool
establishes on the server side a dedicated broker connection (as defined
previously) devoted to carrying all the messages to be exchanged with
the target MQTT server.

</div>

<div class="paragraph">

In the following deployment example, four dedicated broker connections
are activated to support the same number of `MqttClient` instances (and
relative MQTT channels).

</div>

<div class="imageblock" style="text-align: center">

<div class="content">

![dedicated
connections](data:image/svg+xml;base64,PCFET0NUWVBFIHN2ZyBQVUJMSUMgIi0vL1czQy8vRFREIFNWRyAxLjEvL0VOIiAiaHR0cDovL3d3dy53My5vcmcvR3JhcGhpY3MvU1ZHLzEuMS9EVEQvc3ZnMTEuZHRkIj4KPHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHhtbG5zOnhsaW5rPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hsaW5rIiB3aWR0aD0iNzQ1cHgiIGhlaWdodD0iMjc0cHgiIHZlcnNpb249IjEuMSIgc3R5bGU9ImJhY2tncm91bmQtY29sb3I6IHJnYigyNTUsIDI1NSwgMjU1KTsiPjxkZWZzLz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgwLjUsMC41KSI+PHJlY3QgeD0iMCIgeT0iMCIgd2lkdGg9Ijc0NCIgaGVpZ2h0PSIyNzMiIGZpbGw9IiNmZmZmZmYiIHN0cm9rZT0ibm9uZSIgcG9pbnRlci1ldmVudHM9Im5vbmUiLz48cmVjdCB4PSI2MDUiIHk9IjE1MCIgd2lkdGg9IjEwOCIgaGVpZ2h0PSI4MCIgcng9IjEyIiByeT0iMTIiIGZpbGw9IiNjMDc1MWYiIHN0cm9rZT0ibm9uZSIgcG9pbnRlci1ldmVudHM9Im5vbmUiLz48ZyBmaWxsPSIjRkZGRkZGIiBmb250LWZhbWlseT0iSGVsdmV0aWNhIiB0ZXh0LWFuY2hvcj0ibWlkZGxlIiBmb250LXNpemU9IjE0cHgiPjx0ZXh0IHg9IjY1OC41IiB5PSIxOTQuNSI+TVFUVCBCcm9rZXIgMjwvdGV4dD48L2c+PHJlY3QgeD0iMzAiIHk9IjMyIiB3aWR0aD0iMTUyIiBoZWlnaHQ9IjQzIiBmaWxsPSIjMzI5NmMwIiBzdHJva2U9Im5vbmUiIHBvaW50ZXItZXZlbnRzPSJub25lIi8+PGcgZmlsbD0iI0ZGRkZGRiIgZm9udC1mYW1pbHk9IkhlbHZldGljYSIgdGV4dC1hbmNob3I9Im1pZGRsZSIgZm9udC1zaXplPSIxM3B4Ij48dGV4dCB4PSIxMDUuNSIgeT0iNTcuNSI+TXF0dENsaWVudCAxwqB0b8KgQnJva2VyIDE8L3RleHQ+PC9nPjxyZWN0IHg9IjMwIiB5PSI4NiIgd2lkdGg9IjE1MiIgaGVpZ2h0PSI0MyIgZmlsbD0iIzMyOTZjMCIgc3Ryb2tlPSJub25lIiBwb2ludGVyLWV2ZW50cz0ibm9uZSIvPjxnIGZpbGw9IiNGRkZGRkYiIGZvbnQtZmFtaWx5PSJIZWx2ZXRpY2EiIHRleHQtYW5jaG9yPSJtaWRkbGUiIGZvbnQtc2l6ZT0iMTNweCI+PHRleHQgeD0iMTA1LjUiIHk9IjExMS41Ij5NcXR0Q2xpZW50IDIgdG/CoEJyb2tlciAxPC90ZXh0PjwvZz48cmVjdCB4PSIzMCIgeT0iMTM5IiB3aWR0aD0iMTUyIiBoZWlnaHQ9IjQzIiBmaWxsPSIjMzI5NmMwIiBzdHJva2U9Im5vbmUiIHBvaW50ZXItZXZlbnRzPSJub25lIi8+PGcgZmlsbD0iI0ZGRkZGRiIgZm9udC1mYW1pbHk9IkhlbHZldGljYSIgdGV4dC1hbmNob3I9Im1pZGRsZSIgZm9udC1zaXplPSIxM3B4Ij48dGV4dCB4PSIxMDUuNSIgeT0iMTY0LjUiPk1xdHRDbGllbnQgMyB0b8KgQnJva2VyIDI8L3RleHQ+PC9nPjxyZWN0IHg9IjMwIiB5PSIxOTMiIHdpZHRoPSIxNTIiIGhlaWdodD0iNDMiIGZpbGw9IiMzMjk2YzAiIHN0cm9rZT0ibm9uZSIgcG9pbnRlci1ldmVudHM9Im5vbmUiLz48ZyBmaWxsPSIjRkZGRkZGIiBmb250LWZhbWlseT0iSGVsdmV0aWNhIiB0ZXh0LWFuY2hvcj0ibWlkZGxlIiBmb250LXNpemU9IjEzcHgiPjx0ZXh0IHg9IjEwNS41IiB5PSIyMTguNSI+TXF0dENsaWVudCA0IHRvwqBCcm9rZXIgMjwvdGV4dD48L2c+PHJlY3QgeD0iNjA1IiB5PSIzNSIgd2lkdGg9IjEwOCIgaGVpZ2h0PSI4MCIgcng9IjEyIiByeT0iMTIiIGZpbGw9IiNjMDc1MWYiIHN0cm9rZT0ibm9uZSIgcG9pbnRlci1ldmVudHM9Im5vbmUiLz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSg2MTAuNSw2Ny41KSI+PHN3aXRjaD48Zm9yZWlnbk9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6dmlzaWJsZTsiIHBvaW50ZXItZXZlbnRzPSJhbGwiIHdpZHRoPSI5NyIgaGVpZ2h0PSIxNSIgcmVxdWlyZWRGZWF0dXJlcz0iaHR0cDovL3d3dy53My5vcmcvVFIvU1ZHMTEvZmVhdHVyZSNFeHRlbnNpYmlsaXR5Ij48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDE0cHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiByZ2IoMjU1LCAyNTUsIDI1NSk7IGxpbmUtaGVpZ2h0OiAxLjI7IHZlcnRpY2FsLWFsaWduOiB0b3A7IHdoaXRlLXNwYWNlOiBub3dyYXA7IHRleHQtYWxpZ246IGNlbnRlcjsiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OmlubGluZS1ibG9jazt0ZXh0LWFsaWduOmluaGVyaXQ7dGV4dC1kZWNvcmF0aW9uOmluaGVyaXQ7Ij5NUVRUIEJyb2tlciAxPC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0Pjx0ZXh0IHg9IjQ5IiB5PSIxNSIgZmlsbD0iI0ZGRkZGRiIgdGV4dC1hbmNob3I9Im1pZGRsZSIgZm9udC1zaXplPSIxNHB4IiBmb250LWZhbWlseT0iSGVsdmV0aWNhIj5NUVRUIEJyb2tlciAxPC90ZXh0Pjwvc3dpdGNoPjwvZz48ZyBmaWxsPSIjQzA3NTFGIiBmb250LWZhbWlseT0iSGVsdmV0aWNhIiBmb250LXdlaWdodD0iYm9sZCIgZm9udC1zdHlsZT0iaXRhbGljIiB0ZXh0LWFuY2hvcj0ibWlkZGxlIiBmb250LXNpemU9IjExcHgiPjx0ZXh0IHg9IjU4NiIgeT0iMTM5Ij5EZWRpY2F0ZWQgYnJva2VyIGNvbm5lY3Rpb25zPC90ZXh0PjwvZz48cGF0aCBkPSJNIDE5MC43NSA0OS4yMSBMIDE5MC43NCA1My42NyBMIDE4Mi41IDQ4IEwgMTkwLjc3IDQyLjM3IEwgMTkwLjc2IDQ2LjgzIEwgNTk1LjI1IDQ3Ljc5IEwgNTk1LjI2IDQzLjMzIEwgNjAzLjUgNDkgTCA1OTUuMjMgNTQuNjMgTCA1OTUuMjQgNTAuMTcgWiIgZmlsbD0iIzJhNWU3NCIgc3Ryb2tlPSJub25lIiBwb2ludGVyLWV2ZW50cz0ibm9uZSIvPjxwYXRoIGQ9Ik0gMTkwLjc1IDE2Ni4yMSBMIDE5MC43NCAxNzAuNjcgTCAxODIuNSAxNjUgTCAxOTAuNzcgMTU5LjM3IEwgMTkwLjc2IDE2My44MyBMIDU5NS4yNSAxNjQuNzkgTCA1OTUuMjYgMTYwLjMzIEwgNjAzLjUgMTY2IEwgNTk1LjIzIDE3MS42MyBMIDU5NS4yNCAxNjcuMTcgWiIgZmlsbD0iIzJhNWU3NCIgc3Ryb2tlPSJub25lIiBwb2ludGVyLWV2ZW50cz0ibm9uZSIvPjxwYXRoIGQ9Ik0gMTkwLjc1IDEwNi4yMSBMIDE5MC43NCAxMTAuNjcgTCAxODIuNSAxMDUgTCAxOTAuNzcgOTkuMzcgTCAxOTAuNzYgMTAzLjgzIEwgNTk1LjI1IDEwNC43OSBMIDU5NS4yNiAxMDAuMzMgTCA2MDMuNSAxMDYgTCA1OTUuMjMgMTExLjYzIEwgNTk1LjI0IDEwNy4xNyBaIiBmaWxsPSIjMmE1ZTc0IiBzdHJva2U9Im5vbmUiIHBvaW50ZXItZXZlbnRzPSJub25lIi8+PHBhdGggZD0iTSAxOTAuNzUgMjE3LjIxIEwgMTkwLjc0IDIyMS42NyBMIDE4Mi41IDIxNiBMIDE5MC43NyAyMTAuMzcgTCAxOTAuNzYgMjE0LjgzIEwgNTk1LjI1IDIxNS43OSBMIDU5NS4yNiAyMTEuMzMgTCA2MDMuNSAyMTcgTCA1OTUuMjMgMjIyLjYzIEwgNTk1LjI0IDIxOC4xNyBaIiBmaWxsPSIjMmE1ZTc0IiBzdHJva2U9Im5vbmUiIHBvaW50ZXItZXZlbnRzPSJub25lIi8+PHBhdGggZD0iTSA0ODguNzYgNTAuMTkgTCA0ODguNzYgNTQuNjUgTCA0ODAuNSA0OSBMIDQ4OC43NiA0My4zNSBMIDQ4OC43NiA0Ny44MSBMIDU5NS4yNCA0Ny44MSBMIDU5NS4yNCA0My4zNSBMIDYwMy41IDQ5IEwgNTk1LjI0IDU0LjY1IEwgNTk1LjI0IDUwLjE5IFoiIGZpbGw9IiNjMDc1MWYiIHN0cm9rZT0ibm9uZSIgcG9pbnRlci1ldmVudHM9Im5vbmUiLz48cGF0aCBkPSJNIDQ4OC43NiAxMDcuMTkgTCA0ODguNzYgMTExLjY1IEwgNDgwLjUgMTA2IEwgNDg4Ljc2IDEwMC4zNSBMIDQ4OC43NiAxMDQuODEgTCA1OTUuMjQgMTA0LjgxIEwgNTk1LjI0IDEwMC4zNSBMIDYwMy41IDEwNiBMIDU5NS4yNCAxMTEuNjUgTCA1OTUuMjQgMTA3LjE5IFoiIGZpbGw9IiNjMDc1MWYiIHN0cm9rZT0ibm9uZSIgcG9pbnRlci1ldmVudHM9Im5vbmUiLz48cGF0aCBkPSJNIDQ4OC43NiAxNjcuMTkgTCA0ODguNzYgMTcxLjY1IEwgNDgwLjUgMTY2IEwgNDg4Ljc2IDE2MC4zNSBMIDQ4OC43NiAxNjQuODEgTCA1OTUuMjQgMTY0LjgxIEwgNTk1LjI0IDE2MC4zNSBMIDYwMy41IDE2NiBMIDU5NS4yNCAxNzEuNjUgTCA1OTUuMjQgMTY3LjE5IFoiIGZpbGw9IiNjMDc1MWYiIHN0cm9rZT0ibm9uZSIgcG9pbnRlci1ldmVudHM9Im5vbmUiLz48cGF0aCBkPSJNIDQ4OC43NiAyMTguMTkgTCA0ODguNzYgMjIyLjY1IEwgNDgwLjUgMjE3IEwgNDg4Ljc2IDIxMS4zNSBMIDQ4OC43NiAyMTUuODEgTCA1OTUuMjQgMjE1LjgxIEwgNTk1LjI0IDIxMS4zNSBMIDYwMy41IDIxNyBMIDU5NS4yNCAyMjIuNjUgTCA1OTUuMjQgMjE4LjE5IFoiIGZpbGw9IiNjMDc1MWYiIHN0cm9rZT0ibm9uZSIgcG9pbnRlci1ldmVudHM9Im5vbmUiLz48cmVjdCB4PSIyOTUiIHk9IjI4IiB3aWR0aD0iMjA3IiBoZWlnaHQ9IjIxMCIgcng9IjMxLjA1IiByeT0iMzEuMDUiIGZpbGw9IiMyYTVlNzQiIHN0cm9rZT0ibm9uZSIgcG9pbnRlci1ldmVudHM9Im5vbmUiLz48ZyBmaWxsPSIjRkZGRkZGIiBmb250LWZhbWlseT0iSGVsdmV0aWNhIiB0ZXh0LWFuY2hvcj0ibWlkZGxlIiBmb250LXNpemU9IjE3cHgiPjx0ZXh0IHg9IjM5OCIgeT0iMTM5Ij5NUVRULkNvb2w8L3RleHQ+PC9nPjxwYXRoIGQ9Ik0gNTg0LjA3IDEyOSBMIDU2MC4wOSA2MC4wMiIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjYzA3NTFmIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJub25lIi8+PHBhdGggZD0iTSA1NTguMzcgNTUuMDYgTCA1NjMuOTcgNjAuNTIgTCA1NjAuMDkgNjAuMDIgTCA1NTcuMzYgNjIuODIgWiIgZmlsbD0iI2MwNzUxZiIgc3Ryb2tlPSIjYzA3NTFmIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJub25lIi8+PHBhdGggZD0iTSA1NzUuMTYgMTI5IEwgNTUxLjQyIDExNC4zNCIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjYzA3NTFmIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJub25lIi8+PHBhdGggZD0iTSA1NDYuOTUgMTExLjU5IEwgNTU0Ljc1IDExMi4yOSBMIDU1MS40MiAxMTQuMzQgTCA1NTEuMDcgMTE4LjI0IFoiIGZpbGw9IiNjMDc1MWYiIHN0cm9rZT0iI2MwNzUxZiIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0ibm9uZSIvPjxwYXRoIGQ9Ik0gNTg0IDE0NSBMIDU1Ny41OSAyMDQuMTgiIGZpbGw9Im5vbmUiIHN0cm9rZT0iI2MwNzUxZiIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0ibm9uZSIvPjxwYXRoIGQ9Ik0gNTU1LjQ2IDIwOC45OCBMIDU1NS4xMSAyMDEuMTYgTCA1NTcuNTkgMjA0LjE4IEwgNTYxLjUgMjA0LjAxIFoiIGZpbGw9IiNjMDc1MWYiIHN0cm9rZT0iI2MwNzUxZiIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0ibm9uZSIvPjxwYXRoIGQ9Ik0gNTc1LjYgMTQzIEwgNTUxLjM2IDE1OC41NiIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjYzA3NTFmIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJub25lIi8+PHBhdGggZD0iTSA1NDYuOTQgMTYxLjQgTCA1NTAuOTQgMTU0LjY3IEwgNTUxLjM2IDE1OC41NiBMIDU1NC43MiAxNjAuNTYgWiIgZmlsbD0iI2MwNzUxZiIgc3Ryb2tlPSIjYzA3NTFmIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJub25lIi8+PGcgZmlsbD0iIzJBNUU3NCIgZm9udC1mYW1pbHk9IkhlbHZldGljYSIgZm9udC13ZWlnaHQ9ImJvbGQiIGZvbnQtc3R5bGU9Iml0YWxpYyIgdGV4dC1hbmNob3I9Im1pZGRsZSIgZm9udC1zaXplPSIxMXB4Ij48dGV4dCB4PSIyMzgiIHk9IjEzNiI+TVFUVCBjaGFubmVsczwvdGV4dD48L2c+PHBhdGggZD0iTSAyMTQgMTI0IEwgMjIzLjA5IDYxLjMiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzJhNWU3NCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0ibm9uZSIvPjxwYXRoIGQ9Ik0gMjIzLjg0IDU2LjExIEwgMjI2LjMgNjMuNTQgTCAyMjMuMDkgNjEuMyBMIDIxOS4zNyA2Mi41MyBaIiBmaWxsPSIjMmE1ZTc0IiBzdHJva2U9IiMyYTVlNzQiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9Im5vbmUiLz48cGF0aCBkPSJNIDIyNyAxMjIgTCAyNTMuNzMgMTEyLjMxIiBmaWxsPSJub25lIiBzdHJva2U9IiMyYTVlNzQiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9Im5vbmUiLz48cGF0aCBkPSJNIDI1OC42NiAxMTAuNTIgTCAyNTMuMjcgMTE2LjIgTCAyNTMuNzMgMTEyLjMxIEwgMjUwLjg5IDEwOS42MiBaIiBmaWxsPSIjMmE1ZTc0IiBzdHJva2U9IiMyYTVlNzQiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9Im5vbmUiLz48cGF0aCBkPSJNIDIyOCAxNDIgTCAyNDkuODIgMTU2LjM2IiBmaWxsPSJub25lIiBzdHJva2U9IiMyYTVlNzQiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9Im5vbmUiLz48cGF0aCBkPSJNIDI1NC4yMSAxNTkuMjQgTCAyNDYuNDQgMTU4LjMyIEwgMjQ5LjgyIDE1Ni4zNiBMIDI1MC4yOCAxNTIuNDcgWiIgZmlsbD0iIzJhNWU3NCIgc3Ryb2tlPSIjMmE1ZTc0IiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJub25lIi8+PHBhdGggZD0iTSAyMTQgMTQ2LjcxIEwgMjIzLjA1IDIwNi43IiBmaWxsPSJub25lIiBzdHJva2U9IiMyYTVlNzQiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9Im5vbmUiLz48cGF0aCBkPSJNIDIyMy44MyAyMTEuODkgTCAyMTkuMzMgMjA1LjQ5IEwgMjIzLjA1IDIwNi43IEwgMjI2LjI1IDIwNC40NSBaIiBmaWxsPSIjMmE1ZTc0IiBzdHJva2U9IiMyYTVlNzQiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9Im5vbmUiLz48L2c+PC9zdmc+)

</div>

<div class="title">

Figure 8. Dedicated end-to-end connections

</div>

</div>

<div class="paragraph">

Since each broker connection uses the client identifier as sent by the
client, if another `MqttClient` object or any other generic external
MQTT client connects to the same broker using an identical client
identifier, the connection will be closed as per the *MQTT Protocol
Specifications*.

</div>

<div class="paragraph">

By employing a dedicated end-to-end connection, MQTT.Cool guarantees
full support of the following features:

</div>

<div class="ulist">

-   QoS levels 0, 1 and 2

-   persistence of the Session State

-   Will Message

</div>

<div class="admonitionblock note">

  ---- --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  **   The MQTT.Cool server does not take any active roles in the management of the Session State, which is, on the contrary, maintained exclusively by the two ends of the connection, the MQTT broker and `MqttClient`.
  ---- --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

</div>

<div class="sect4">

##### Life-Cycle Events {#_life_cycle_events}

<div class="paragraph">

In a dedicated end-to-end connection, the life-cycle events relative to
`MqttClient`, MQTT channel and dedicated broker connection are tied
together, namely:

</div>

<div class="ulist">

-   A connection request initiated by `MqttClient`, which means a newly
    created MQTT channel, will be propagated up to the MQTT broker,
    through the establishment of a new dedicated broker connection.

-   A disconnection request initiated by `MqttClient`, which means the
    closure of the MQTT channel, will be propagated up to the MQTT
    broker, which in turn will close the dedicated broker connection.

-   An interruption of the dedicated broker connection (due to any
    network issue or to problem in the MQTT broker process) will be
    propagated back to `MqttClient`, which in turn will disconnect from
    MQTT.Cool by closing the MQTT channel.

-   An interruption of the MQTT.Cool connection on the client side (due
    to any network issue or to an explicit `MQTTCoolSession` closing)
    will be propagated up to the MQTT broker by shutting down the
    dedicated broker connection.

-   Any MQTT.Cool server failure will cause the interruption of both the
    dedicated broker connection on the server side and the MQTT.Cool
    connection on the client side.

</div>

<div class="admonitionblock note">

  ---- --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  **   Any issue on the MQTT.Cool connection detected on the client side will cause the `MqttClient` instance to try a reconnection (as you will see in [Section 3.12, “Reconnecting”](#reconnecting)).
  ---- --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

</div>

</div>

</div>

<div class="sect3">

#### 3.6.3. Shared End-to-End Connection {#shared_connection}

<div class="paragraph">

A shared end-to-end connection is realized when MQTT.Cool holds a single
broker connection that will be shared among all those `MqttClient`
instances (even hosted on different network locations) with the
following common characteristics:

</div>

<div class="olist arabic">

1.  No client identifier has been passed at the time of creation from
    `MQTTCoolSession`.

2.  Connect to the same MQTT broker, along with identical username and
    password, if any (by providing a set of connection options, as will
    be detailed further on).

</div>

<div class="paragraph">

From the following diagram, you can see how the MQTT.Cool server
*logically* joins together separate MQTT channels targeted to the same
MQTT broker into single broker connections, namely:

</div>

<div class="ulist">

-   The MQTT channels initiated by `MqttClient` 1 and 2 joined into the
    broker connection to "MQTT Broker A".

-   The MQTT channels initiated by `MqttClient` 3 and 4 joined into the
    broker connection to "MQTT Broker B".

</div>

<div class="imageblock" style="text-align: center">

<div class="content">

![shared
connections](data:image/svg+xml;base64,PCFET0NUWVBFIHN2ZyBQVUJMSUMgIi0vL1czQy8vRFREIFNWRyAxLjEvL0VOIiAiaHR0cDovL3d3dy53My5vcmcvR3JhcGhpY3MvU1ZHLzEuMS9EVEQvc3ZnMTEuZHRkIj4KPHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHhtbG5zOnhsaW5rPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hsaW5rIiB3aWR0aD0iNzQ1cHgiIGhlaWdodD0iMjc0cHgiIHZlcnNpb249IjEuMSIgc3R5bGU9ImJhY2tncm91bmQtY29sb3I6IHJnYigyNTUsIDI1NSwgMjU1KTsiPjxkZWZzLz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgwLjUsMC41KSI+PHJlY3QgeD0iMCIgeT0iMCIgd2lkdGg9Ijc0NCIgaGVpZ2h0PSIyNzMiIGZpbGw9IiNmZmZmZmYiIHN0cm9rZT0ibm9uZSIgcG9pbnRlci1ldmVudHM9Im5vbmUiLz48cGF0aCBkPSJNIDM5MC41IDc2LjE5IEwgMzkwLjUgNzMuODEgTCA1OTYuMjQgNzMuODEgTCA1OTYuMjQgNjkuMzUgTCA2MDQuNSA3NSBMIDU5Ni4yNCA4MC42NSBMIDU5Ni4yNCA3Ni4xOSBaIiBmaWxsPSIjYzA3NTFmIiBzdHJva2U9Im5vbmUiIHBvaW50ZXItZXZlbnRzPSJub25lIi8+PHBhdGggZD0iTSAxOTAuNzYgMTA2LjE5IEwgMTkwLjc2IDExMC42NSBMIDE4Mi41IDEwNSBMIDE5MC43NiA5OS4zNSBMIDE5MC43NiAxMDMuODEgTCAzNzkuODEgMTAzLjgxIEwgMzc5LjgxIDkxLjc2IEwgMzc1LjM1IDkxLjc2IEwgMzgxIDgzLjUgTCAzODYuNjUgOTEuNzYgTCAzODIuMTkgOTEuNzYgTCAzODIuMTkgMTAzLjgxIFEgMzgyLjE5IDEwNi4xOSAzNzkuODEgMTA2LjE5IFoiIGZpbGw9IiMyYTVlNzQiIHN0cm9rZT0ibm9uZSIgcG9pbnRlci1ldmVudHM9Im5vbmUiLz48cGF0aCBkPSJNIDE5MC43NiA1MC4xNSBMIDE5MC43OCA1NC42IEwgMTgyLjUgNDkgTCAxOTAuNzMgNDMuMzEgTCAxOTAuNzUgNDcuNzcgTCAzODUuODQgNDYuODIgUSAzODguMTQgNDYuOCAzODguMjQgNDkuMSBMIDM4OC44NCA2NC4yIEwgMzkzLjI5IDY0LjAyIEwgMzg3Ljk4IDcyLjUgTCAzODIuMDEgNjQuNDggTCAzODYuNDYgNjQuMyBMIDM4NS44NiA0OS4yIFoiIGZpbGw9IiMyYTVlNzQiIHN0cm9rZT0ibm9uZSIgcG9pbnRlci1ldmVudHM9Im5vbmUiLz48cmVjdCB4PSI2MDUiIHk9IjE0OSIgd2lkdGg9IjEwOCIgaGVpZ2h0PSI4MCIgcng9IjEyIiByeT0iMTIiIGZpbGw9IiNjMDc1MWYiIHN0cm9rZT0ibm9uZSIgcG9pbnRlci1ldmVudHM9Im5vbmUiLz48ZyBmaWxsPSIjRkZGRkZGIiBmb250LWZhbWlseT0iSGVsdmV0aWNhIiB0ZXh0LWFuY2hvcj0ibWlkZGxlIiBmb250LXNpemU9IjE0cHgiPjx0ZXh0IHg9IjY1OC41IiB5PSIxOTMuNSI+TVFUVCBCcm9rZXIgQjwvdGV4dD48L2c+PHJlY3QgeD0iMzAiIHk9IjI3IiB3aWR0aD0iMTUyIiBoZWlnaHQ9IjQzIiBmaWxsPSIjMzI5NmMwIiBzdHJva2U9Im5vbmUiIHBvaW50ZXItZXZlbnRzPSJub25lIi8+PGcgZmlsbD0iI0ZGRkZGRiIgZm9udC1mYW1pbHk9IkhlbHZldGljYSIgdGV4dC1hbmNob3I9Im1pZGRsZSIgZm9udC1zaXplPSIxM3B4Ij48dGV4dCB4PSIxMDUuNSIgeT0iNTIuNSI+TXF0dENsaWVudCAxwqB0b8KgQnJva2VyIEE8L3RleHQ+PC9nPjxyZWN0IHg9IjMwIiB5PSI4MyIgd2lkdGg9IjE1MiIgaGVpZ2h0PSI0MyIgZmlsbD0iIzMyOTZjMCIgc3Ryb2tlPSJub25lIiBwb2ludGVyLWV2ZW50cz0ibm9uZSIvPjxnIGZpbGw9IiNGRkZGRkYiIGZvbnQtZmFtaWx5PSJIZWx2ZXRpY2EiIHRleHQtYW5jaG9yPSJtaWRkbGUiIGZvbnQtc2l6ZT0iMTNweCI+PHRleHQgeD0iMTA1LjUiIHk9IjEwOC41Ij5NcXR0Q2xpZW50IDIgdG/CoEJyb2tlciBBPC90ZXh0PjwvZz48cmVjdCB4PSIzMCIgeT0iMTQzIiB3aWR0aD0iMTUyIiBoZWlnaHQ9IjQzIiBmaWxsPSIjMzI5NmMwIiBzdHJva2U9Im5vbmUiIHBvaW50ZXItZXZlbnRzPSJub25lIi8+PGcgZmlsbD0iI0ZGRkZGRiIgZm9udC1mYW1pbHk9IkhlbHZldGljYSIgdGV4dC1hbmNob3I9Im1pZGRsZSIgZm9udC1zaXplPSIxM3B4Ij48dGV4dCB4PSIxMDUuNSIgeT0iMTY4LjUiPk1xdHRDbGllbnQgMyB0b8KgQnJva2VyIEI8L3RleHQ+PC9nPjxyZWN0IHg9IjMwIiB5PSIxOTMiIHdpZHRoPSIxNTIiIGhlaWdodD0iNDMiIGZpbGw9IiMzMjk2YzAiIHN0cm9rZT0ibm9uZSIgcG9pbnRlci1ldmVudHM9Im5vbmUiLz48ZyBmaWxsPSIjRkZGRkZGIiBmb250LWZhbWlseT0iSGVsdmV0aWNhIiB0ZXh0LWFuY2hvcj0ibWlkZGxlIiBmb250LXNpemU9IjEzcHgiPjx0ZXh0IHg9IjEwNS41IiB5PSIyMTguNSI+TXF0dENsaWVudCA0IHRvwqBCcm9rZXIgQjwvdGV4dD48L2c+PHJlY3QgeD0iNjA1IiB5PSIzNSIgd2lkdGg9IjEwOCIgaGVpZ2h0PSI4MCIgcng9IjEyIiByeT0iMTIiIGZpbGw9IiNjMDc1MWYiIHN0cm9rZT0ibm9uZSIgcG9pbnRlci1ldmVudHM9Im5vbmUiLz48ZyBmaWxsPSIjRkZGRkZGIiBmb250LWZhbWlseT0iSGVsdmV0aWNhIiB0ZXh0LWFuY2hvcj0ibWlkZGxlIiBmb250LXNpemU9IjE0cHgiPjx0ZXh0IHg9IjY1OC41IiB5PSI3OS41Ij5NUVRUIEJyb2tlciBBPC90ZXh0PjwvZz48ZyBmaWxsPSIjQzA3NTFGIiBmb250LWZhbWlseT0iSGVsdmV0aWNhIiBmb250LXdlaWdodD0iYm9sZCIgZm9udC1zdHlsZT0iaXRhbGljIiB0ZXh0LWFuY2hvcj0ibWlkZGxlIiBmb250LXNpemU9IjExcHgiPjx0ZXh0IHg9IjU4NiIgeT0iMTM5Ij5TaGFyZWQgYnJva2VyIGNvbm5lY3Rpb25zPC90ZXh0PjwvZz48cGF0aCBkPSJNIDE5MC43NiAxNjYuMTkgTCAxOTAuNzYgMTcwLjY1IEwgMTgyLjUgMTY1IEwgMTkwLjc2IDE1OS4zNSBMIDE5MC43NiAxNjMuODEgTCAzODIuMjQgMTYzLjgxIEwgMzgyLjI0IDE1OS4zNSBMIDM5MC41IDE2NSBMIDM4Mi4yNCAxNzAuNjUgTCAzODIuMjQgMTY2LjE5IFoiIGZpbGw9IiMyYTVlNzQiIHN0cm9rZT0ibm9uZSIgcG9pbnRlci1ldmVudHM9Im5vbmUiLz48cGF0aCBkPSJNIDE5MC43NiAyMTcuMTkgTCAxOTAuNzYgMjIxLjY1IEwgMTgyLjUgMjE2IEwgMTkwLjc2IDIxMC4zNSBMIDE5MC43NiAyMTQuODEgTCAzNzQuMjQgMjE0LjgxIEwgMzc0LjI0IDIxMC4zNSBMIDM4Mi41IDIxNiBMIDM3NC4yNCAyMjEuNjUgTCAzNzQuMjQgMjE3LjE5IFoiIGZpbGw9IiMyYTVlNzQiIHN0cm9rZT0ibm9uZSIgcG9pbnRlci1ldmVudHM9Im5vbmUiLz48cGF0aCBkPSJNIDUwMS41IDE5MC4xOSBMIDUwMS41IDE4Ny44MSBMIDU5Ni4yNCAxODcuODEgTCA1OTYuMjQgMTgzLjM1IEwgNjA0LjUgMTg5IEwgNTk2LjI0IDE5NC42NSBMIDU5Ni4yNCAxOTAuMTkgWiIgZmlsbD0iI2MwNzUxZiIgc3Ryb2tlPSJub25lIiBwb2ludGVyLWV2ZW50cz0ibm9uZSIvPjxyZWN0IHg9IjI5NSIgeT0iMjgiIHdpZHRoPSIyMDciIGhlaWdodD0iMjEwIiByeD0iMzEuMDUiIHJ5PSIzMS4wNSIgZmlsbD0iIzJhNWU3NCIgc3Ryb2tlPSJub25lIiBwb2ludGVyLWV2ZW50cz0ibm9uZSIvPjxnIGZpbGw9IiNGRkZGRkYiIGZvbnQtZmFtaWx5PSJIZWx2ZXRpY2EiIHRleHQtYW5jaG9yPSJtaWRkbGUiIGZvbnQtc2l6ZT0iMTdweCI+PHRleHQgeD0iMzk4IiB5PSIxMzkiPk1RVFQuQ29vbDwvdGV4dD48L2c+PHBhdGggZD0iTSA1ODIuNDkgMTI5IEwgNTU4LjE2IDg2LjUzIiBmaWxsPSJub25lIiBzdHJva2U9IiNjMDc1MWYiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9Im5vbmUiLz48cGF0aCBkPSJNIDU1NS41NiA4MS45NyBMIDU2Mi4wNyA4Ni4zIEwgNTU4LjE2IDg2LjUzIEwgNTU2IDg5Ljc4IFoiIGZpbGw9IiNjMDc1MWYiIHN0cm9rZT0iI2MwNzUxZiIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0ibm9uZSIvPjxwYXRoIGQ9Ik0gNTg0IDE0NSBMIDU1OC42OCAxODAuOCIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjYzA3NTFmIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJub25lIi8+PHBhdGggZD0iTSA1NTUuNjUgMTg1LjA5IEwgNTU2LjgzIDE3Ny4zNSBMIDU1OC42OCAxODAuOCBMIDU2Mi41NSAxODEuMzkgWiIgZmlsbD0iI2MwNzUxZiIgc3Ryb2tlPSIjYzA3NTFmIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJub25lIi8+PHBhdGggZD0iTSAyOTcuOTUgNDkuMyBMIDI5Ny45NCA0Ni45MiBMIDM4OC44MSA0Ni44MSBRIDM5MS4xOSA0Ni44MSAzOTEuMTkgNDkuMTkgTCAzOTEuMTkgNzQuMyBMIDM4OC44MSA3NC4zIEwgMzg4LjgxIDQ5LjE5IFoiIGZpbGw9IiM1OWEyYzAiIHN0cm9rZT0iI2MwNzUxZiIgc3Ryb2tlLWxpbmVqb2luPSJyb3VuZCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBzdHJva2UtZGFzaGFycmF5PSIzIDMiIHBvaW50ZXItZXZlbnRzPSJub25lIi8+PHBhdGggZD0iTSAyOTQuNSAxMDYuMTkgTCAyOTQuNSAxMDMuODEgTCAzODguODEgMTAzLjgxIEwgMzg4LjgxIDc1LjUgTCAzOTEuMTkgNzUuNSBMIDM5MS4xOSAxMDMuODEgUSAzOTEuMTkgMTA2LjE5IDM4OC44MSAxMDYuMTkgWiIgZmlsbD0iIzU5YTJjMCIgc3Ryb2tlPSIjZGM5YzgwIiBzdHJva2UtbGluZWpvaW49InJvdW5kIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHN0cm9rZS1kYXNoYXJyYXk9IjMgMyIgcG9pbnRlci1ldmVudHM9Im5vbmUiLz48cGF0aCBkPSJNIDM4OC41IDc2LjE5IEwgMzg4LjUgNzMuODEgTCA1MDMuNSA3My44MSBMIDUwMy41IDc2LjE5IFoiIGZpbGw9IiNjMDc1MWYiIHN0cm9rZT0iI2RjOWM4MCIgc3Ryb2tlLWxpbmVqb2luPSJyb3VuZCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBzdHJva2UtZGFzaGFycmF5PSIzIDMiIHBvaW50ZXItZXZlbnRzPSJub25lIi8+PHBhdGggZD0iTSAyOTQuOSAyMTcuMzkgTCAyOTQuOSAyMTUuMDEgTCAzODguODEgMjE0LjgxIEwgMzg4LjgxIDE4Ni41IEwgMzkxLjE5IDE4Ni41IEwgMzkxLjE5IDIxNC44MSBRIDM5MS4xOSAyMTcuMTkgMzg4LjgxIDIxNy4xOSBaIiBmaWxsPSIjNTlhMmMwIiBzdHJva2U9IiNjMDc1MWYiIHN0cm9rZS1saW5lam9pbj0icm91bmQiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgc3Ryb2tlLWRhc2hhcnJheT0iMyAzIiBwb2ludGVyLWV2ZW50cz0ibm9uZSIvPjxwYXRoIGQ9Ik0gMjk1LjUgMTY1LjE5IEwgMjk1LjUgMTYyLjgxIEwgMzg4LjgxIDE2Mi44MSBRIDM5MS4xOSAxNjIuODEgMzkxLjE5IDE2NS4xOSBMIDM5MS4xOSAxODguMyBMIDM4OC44MSAxODguMyBMIDM4OC44MSAxNjUuMTkgWiIgZmlsbD0iIzU5YTJjMCIgc3Ryb2tlPSIjYzA3NTFmIiBzdHJva2UtbGluZWpvaW49InJvdW5kIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHN0cm9rZS1kYXNoYXJyYXk9IjMgMyIgcG9pbnRlci1ldmVudHM9Im5vbmUiLz48cGF0aCBkPSJNIDM5MS41IDE5MC4xOSBMIDM5MS41IDE4Ny44MSBMIDUwNi41IDE4Ny44MSBMIDUwNi41IDE5MC4xOSBaIiBmaWxsPSIjYzA3NTFmIiBzdHJva2U9IiNkYzljODAiIHN0cm9rZS1saW5lam9pbj0icm91bmQiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgc3Ryb2tlLWRhc2hhcnJheT0iMyAzIiBwb2ludGVyLWV2ZW50cz0ibm9uZSIvPjxnIGZpbGw9IiMyQTVFNzQiIGZvbnQtZmFtaWx5PSJIZWx2ZXRpY2EiIGZvbnQtd2VpZ2h0PSJib2xkIiBmb250LXN0eWxlPSJpdGFsaWMiIHRleHQtYW5jaG9yPSJtaWRkbGUiIGZvbnQtc2l6ZT0iMTFweCI+PHRleHQgeD0iMjM4IiB5PSIxMzYiPk1RVFQgY2hhbm5lbHM8L3RleHQ+PC9nPjxwYXRoIGQ9Ik0gMjE0IDEyNCBMIDIyMy4wOSA2MS4zIiBmaWxsPSJub25lIiBzdHJva2U9IiMyYTVlNzQiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9Im5vbmUiLz48cGF0aCBkPSJNIDIyMy44NCA1Ni4xMSBMIDIyNi4zIDYzLjU0IEwgMjIzLjA5IDYxLjMgTCAyMTkuMzcgNjIuNTMgWiIgZmlsbD0iIzJhNWU3NCIgc3Ryb2tlPSIjMmE1ZTc0IiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJub25lIi8+PHBhdGggZD0iTSAyMjcgMTIyIEwgMjU0LjAyIDExMi4xOCIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMmE1ZTc0IiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJub25lIi8+PHBhdGggZD0iTSAyNTguOTUgMTEwLjM4IEwgMjUzLjU3IDExNi4wNiBMIDI1NC4wMiAxMTIuMTggTCAyNTEuMTcgMTA5LjQ4IFoiIGZpbGw9IiMyYTVlNzQiIHN0cm9rZT0iIzJhNWU3NCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0ibm9uZSIvPjxwYXRoIGQ9Ik0gMjI4IDE0MiBMIDI0OS43IDE1Ni40NyIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMmE1ZTc0IiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJub25lIi8+PHBhdGggZD0iTSAyNTQuMDcgMTU5LjM4IEwgMjQ2LjMgMTU4LjQxIEwgMjQ5LjcgMTU2LjQ3IEwgMjUwLjE5IDE1Mi41OCBaIiBmaWxsPSIjMmE1ZTc0IiBzdHJva2U9IiMyYTVlNzQiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9Im5vbmUiLz48cGF0aCBkPSJNIDIxNCAxNDcgTCAyMjMuMDUgMjA2LjciIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzJhNWU3NCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0ibm9uZSIvPjxwYXRoIGQ9Ik0gMjIzLjgzIDIxMS44OSBMIDIxOS4zMiAyMDUuNSBMIDIyMy4wNSAyMDYuNyBMIDIyNi4yNCAyMDQuNDUgWiIgZmlsbD0iIzJhNWU3NCIgc3Ryb2tlPSIjMmE1ZTc0IiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJub25lIi8+PHBhdGggZD0iTSAyMzkgMTQwIFEgMjM5IDE0MCAyMzkgMTQwIiBmaWxsPSJub25lIiBzdHJva2U9IiMyYTVlNzQiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgc3Ryb2tlLWRhc2hhcnJheT0iMSAxIiBwb2ludGVyLWV2ZW50cz0ibm9uZSIvPjxwYXRoIGQ9Ik0gMjM5IDE0MCBMIDIzOSAxNDAgTCAyMzkgMTQwIEwgMjM5IDE0MCBaIiBmaWxsPSIjMmE1ZTc0IiBzdHJva2U9IiMyYTVlNzQiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9Im5vbmUiLz48L2c+PC9zdmc+)

</div>

<div class="title">

Figure 9. Shared end-to-end connections

</div>

</div>

<div class="paragraph">

By exploiting this mechanism, MQTT.Cool drastically reduces the amount
of newly created MQTT connections to the broker, with the purpose of
optimizing the server side resources: from the above example, the number
of physical MQTT connections required to serve all the `MqttClient`
instances is halved with respect to the *dedicated* scenario.

</div>

<div class="admonitionblock note">

  ---- ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  **   While joining them into shared broker connections, the MQTT.Cool server takes in considerations only activated MQTT channels, regardless of the MQTT.Cool connections on the client side they have been multiplexed into.
  ---- ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

</div>

<div class="paragraph">

Furthermore, all the subscriptions to the same topic filter will be
logically *merged* into one single MQTT subscription, which is actually
activated on the shared broker connection. This enables offloading the
fan out to MQTT.Cool, as it will be responsible for propagating messages
flowing on the MQTT channel up to all subscribing clients.

</div>

<div class="paragraph">

The picture below shows an example in which a message targeted to
`cool/topic` is initially published by an external MQTT client to the
MQTT broker.

</div>

<div class="imageblock" style="text-align: center">

<div class="content">

![shared
subscriptions](data:image/svg+xml;base64,PCFET0NUWVBFIHN2ZyBQVUJMSUMgIi0vL1czQy8vRFREIFNWRyAxLjEvL0VOIiAiaHR0cDovL3d3dy53My5vcmcvR3JhcGhpY3MvU1ZHLzEuMS9EVEQvc3ZnMTEuZHRkIj4KPHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHhtbG5zOnhsaW5rPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hsaW5rIiB3aWR0aD0iODYxcHgiIGhlaWdodD0iMzM3cHgiIHZlcnNpb249IjEuMSIgc3R5bGU9ImJhY2tncm91bmQtY29sb3I6IHJnYigyNTUsIDI1NSwgMjU1KTsiPjxkZWZzLz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgwLjUsMC41KSI+PHJlY3QgeD0iMCIgeT0iMCIgd2lkdGg9Ijg2MCIgaGVpZ2h0PSIzMzYiIGZpbGw9IiNmZmZmZmYiIHN0cm9rZT0ibm9uZSIgcG9pbnRlci1ldmVudHM9Im5vbmUiLz48cmVjdCB4PSIxMCIgeT0iNDEiIHdpZHRoPSIxNjAiIGhlaWdodD0iMjMzIiByeD0iMjQiIHJ5PSIyNCIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjNTlhMmMwIiBwb2ludGVyLWV2ZW50cz0ibm9uZSIvPjxnIGZpbGw9IiM1OUEyQzAiIGZvbnQtZmFtaWx5PSJIZWx2ZXRpY2EiIGZvbnQtd2VpZ2h0PSJib2xkIiB0ZXh0LWFuY2hvcj0ibWlkZGxlIiBmb250LXNpemU9IjEzcHgiPjx0ZXh0IHg9Ijg5LjUiIHk9IjIzOS41Ij5DbGllbnRzIHNoYXJpbmfCoDwvdGV4dD48dGV4dCB4PSI4OS41IiB5PSIyNTUuNSI+dGhlIGNvbm5lY3Rpb248L3RleHQ+PC9nPjxwYXRoIGQ9Ik0gNzUxIDE0MC42NiBMIDY1OC43NCAxNDAuMDUiIGZpbGw9Im5vbmUiIHN0cm9rZT0iI2MwNzUxZiIgc3Ryb2tlLXdpZHRoPSIyIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHN0cm9rZS1kYXNoYXJyYXk9IjIgMiIgcG9pbnRlci1ldmVudHM9Im5vbmUiLz48cGF0aCBkPSJNIDY1NC4yNCAxNDAuMDIgTCA2NjAuMjYgMTM3LjA2IEwgNjU4Ljc0IDE0MC4wNSBMIDY2MC4yMiAxNDMuMDYgWiIgZmlsbD0iI2MwNzUxZiIgc3Ryb2tlPSIjYzA3NTFmIiBzdHJva2Utd2lkdGg9IjIiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9Im5vbmUiLz48cmVjdCB4PSI3NTEiIHk9IjEyMSIgd2lkdGg9IjEwMCIgaGVpZ2h0PSI0MCIgZmlsbD0iIzc0NTIyYSIgc3Ryb2tlPSJub25lIiBwb2ludGVyLWV2ZW50cz0ibm9uZSIvPjxnIGZpbGw9IiNGRkZGRkYiIGZvbnQtZmFtaWx5PSJIZWx2ZXRpY2EiIHRleHQtYW5jaG9yPSJtaWRkbGUiIGZvbnQtc2l6ZT0iMTJweCI+PHRleHQgeD0iODAwLjUiIHk9IjE0NC41Ij5NUVRUIENsaWVudDwvdGV4dD48L2c+PHBhdGggZD0iTSAzMTggMTk0IEwgMzE4IDI1Ny4yNiIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMmE1ZTc0IiBzdHJva2Utd2lkdGg9IjIiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgc3Ryb2tlLWRhc2hhcnJheT0iMiAyIiBwb2ludGVyLWV2ZW50cz0ibm9uZSIvPjxwYXRoIGQ9Ik0gMzE4IDI2MS43NiBMIDMxNSAyNTUuNzYgTCAzMTggMjU3LjI2IEwgMzIxIDI1NS43NiBaIiBmaWxsPSIjMmE1ZTc0IiBzdHJva2U9IiMyYTVlNzQiIHN0cm9rZS13aWR0aD0iMiIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0ibm9uZSIvPjxwYXRoIGQ9Ik0gMjQ4IDE2NyBMIDE0Ny41NiAxOTAuNDciIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzJhNWU3NCIgc3Ryb2tlLXdpZHRoPSIyIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHN0cm9rZS1kYXNoYXJyYXk9IjIgMiIgcG9pbnRlci1ldmVudHM9Im5vbmUiLz48cGF0aCBkPSJNIDE0My4xOCAxOTEuNDkgTCAxNDguMzQgMTg3LjIgTCAxNDcuNTYgMTkwLjQ3IEwgMTQ5LjcgMTkzLjA1IFoiIGZpbGw9IiMyYTVlNzQiIHN0cm9rZT0iIzJhNWU3NCIgc3Ryb2tlLXdpZHRoPSIyIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJub25lIi8+PHJlY3QgeD0iMjQ4IiB5PSI4NyIgd2lkdGg9IjE0MCIgaGVpZ2h0PSIxMDciIHJ4PSIxNi4wNSIgcnk9IjE2LjA1IiBmaWxsPSIjMmE1ZTc0IiBzdHJva2U9Im5vbmUiIHBvaW50ZXItZXZlbnRzPSJub25lIi8+PGcgZmlsbD0iI0ZGRkZGRiIgZm9udC1mYW1pbHk9IkhlbHZldGljYSIgdGV4dC1hbmNob3I9Im1pZGRsZSIgZm9udC1zaXplPSIxN3B4Ij48dGV4dCB4PSIzMTYuNSIgeT0iMTQ2LjUiPk1RVFQuQ29vbDwvdGV4dD48L2c+PHBhdGggZD0iTSAyNDggMTQxIEwgMTQ3LjczIDEzOC4xOSIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMmE1ZTc0IiBzdHJva2Utd2lkdGg9IjIiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgc3Ryb2tlLWRhc2hhcnJheT0iMiAyIiBwb2ludGVyLWV2ZW50cz0ibm9uZSIvPjxwYXRoIGQ9Ik0gMTQzLjI0IDEzOC4wNiBMIDE0OS4zMiAxMzUuMjMgTCAxNDcuNzMgMTM4LjE5IEwgMTQ5LjE1IDE0MS4yMyBaIiBmaWxsPSIjMmE1ZTc0IiBzdHJva2U9IiMyYTVlNzQiIHN0cm9rZS13aWR0aD0iMiIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0ibm9uZSIvPjxyZWN0IHg9IjU1MiIgeT0iMTAwIiB3aWR0aD0iMTAwIiBoZWlnaHQ9IjgwIiByeD0iMTIiIHJ5PSIxMiIgZmlsbD0iI2MwNzUxZiIgc3Ryb2tlPSJub25lIiBwb2ludGVyLWV2ZW50cz0ibm9uZSIvPjxnIGZpbGw9IiNGRkZGRkYiIGZvbnQtZmFtaWx5PSJIZWx2ZXRpY2EiIHRleHQtYW5jaG9yPSJtaWRkbGUiIGZvbnQtc2l6ZT0iMTRweCI+PHRleHQgeD0iNjAxLjUiIHk9IjE0NC41Ij5NUVRUIEJyb2tlcjwvdGV4dD48L2c+PHJlY3QgeD0iMzkiIHk9IjYzIiB3aWR0aD0iMTAyIiBoZWlnaHQ9IjQzIiBmaWxsPSIjMzI5NmMwIiBzdHJva2U9Im5vbmUiIHBvaW50ZXItZXZlbnRzPSJub25lIi8+PGcgZmlsbD0iI0ZGRkZGRiIgZm9udC1mYW1pbHk9IkhlbHZldGljYSIgdGV4dC1hbmNob3I9Im1pZGRsZSIgZm9udC1zaXplPSIxMnB4Ij48dGV4dCB4PSI4OS41IiB5PSI4MSI+TXF0dENsaWVudCAxPC90ZXh0Pjx0ZXh0IHg9Ijg5LjUiIHk9Ijk1Ij4iY29vbC90b3BpYzwvdGV4dD48L2c+PHJlY3QgeD0iMzkiIHk9IjExNiIgd2lkdGg9IjEwMiIgaGVpZ2h0PSI0MyIgZmlsbD0iIzMyOTZjMCIgc3Ryb2tlPSJub25lIiBwb2ludGVyLWV2ZW50cz0ibm9uZSIvPjxnIGZpbGw9IiNGRkZGRkYiIGZvbnQtZmFtaWx5PSJIZWx2ZXRpY2EiIHRleHQtYW5jaG9yPSJtaWRkbGUiIGZvbnQtc2l6ZT0iMTJweCI+PHRleHQgeD0iODkuNSIgeT0iMTM0Ij5NcXR0Q2xpZW50IDI8L3RleHQ+PHRleHQgeD0iODkuNSIgeT0iMTQ4Ij4iY29vbC90b3BpYyI8L3RleHQ+PC9nPjxwYXRoIGQ9Ik0gNTUyIDE2MCBMIDM5NC43NCAxNjAiIGZpbGw9Im5vbmUiIHN0cm9rZT0iI2MwNzUxZiIgc3Ryb2tlLXdpZHRoPSIyIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHN0cm9rZS1kYXNoYXJyYXk9IjIgMiIgcG9pbnRlci1ldmVudHM9Im5vbmUiLz48cGF0aCBkPSJNIDM5MC4yNCAxNjAgTCAzOTYuMjQgMTU3IEwgMzk0Ljc0IDE2MCBMIDM5Ni4yNCAxNjMgWiIgZmlsbD0iI2MwNzUxZiIgc3Ryb2tlPSIjYzA3NTFmIiBzdHJva2Utd2lkdGg9IjIiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9Im5vbmUiLz48cGF0aCBkPSJNIDI0OCAxMTQgTCAxNDcuNSA4Ni43NiIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMmE1ZTc0IiBzdHJva2Utd2lkdGg9IjIiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgc3Ryb2tlLWRhc2hhcnJheT0iMiAyIiBwb2ludGVyLWV2ZW50cz0ibm9uZSIvPjxwYXRoIGQ9Ik0gMTQzLjE2IDg1LjU4IEwgMTQ5LjczIDg0LjI2IEwgMTQ3LjUgODYuNzYgTCAxNDguMTYgOTAuMDUgWiIgZmlsbD0iIzJhNWU3NCIgc3Ryb2tlPSIjMmE1ZTc0IiBzdHJva2Utd2lkdGg9IjIiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9Im5vbmUiLz48cGF0aCBkPSJNIDU1MiAxMjAgTCAzOTQuNzQgMTIwIiBmaWxsPSJub25lIiBzdHJva2U9IiNjMDc1MWYiIHN0cm9rZS13aWR0aD0iMiIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBzdHJva2UtZGFzaGFycmF5PSIyIDIiIHBvaW50ZXItZXZlbnRzPSJub25lIi8+PHBhdGggZD0iTSAzOTAuMjQgMTIwIEwgMzk2LjI0IDExNyBMIDM5NC43NCAxMjAgTCAzOTYuMjQgMTIzIFoiIGZpbGw9IiNjMDc1MWYiIHN0cm9rZT0iI2MwNzUxZiIgc3Ryb2tlLXdpZHRoPSIyIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJub25lIi8+PHJlY3QgeD0iMjY3IiB5PSIyNjQiIHdpZHRoPSIxMDIiIGhlaWdodD0iNDMiIGZpbGw9IiMzMjk2YzAiIHN0cm9rZT0ibm9uZSIgcG9pbnRlci1ldmVudHM9Im5vbmUiLz48ZyBmaWxsPSIjRkZGRkZGIiBmb250LWZhbWlseT0iSGVsdmV0aWNhIiB0ZXh0LWFuY2hvcj0ibWlkZGxlIiBmb250LXNpemU9IjEycHgiPjx0ZXh0IHg9IjMxNy41IiB5PSIyODIiPk1xdHRDbGllbnQgNDwvdGV4dD48dGV4dCB4PSIzMTcuNSIgeT0iMjk2Ij4iY29vbC90b3BpYyI8L3RleHQ+PC9nPjxyZWN0IHg9IjM5IiB5PSIxNzAiIHdpZHRoPSIxMDIiIGhlaWdodD0iNDMiIGZpbGw9IiMzMjk2YzAiIHN0cm9rZT0ibm9uZSIgcG9pbnRlci1ldmVudHM9Im5vbmUiLz48ZyBmaWxsPSIjRkZGRkZGIiBmb250LWZhbWlseT0iSGVsdmV0aWNhIiB0ZXh0LWFuY2hvcj0ibWlkZGxlIiBmb250LXNpemU9IjEycHgiPjx0ZXh0IHg9Ijg5LjUiIHk9IjE4OCI+TXF0dENsaWVudCAzPC90ZXh0Pjx0ZXh0IHg9Ijg5LjUiIHk9IjIwMiI+ImNvb2wvdG9waWMiPC90ZXh0PjwvZz48ZyBmaWxsPSIjQzA3NTFGIiBmb250LWZhbWlseT0iSGVsdmV0aWNhIiB0ZXh0LWFuY2hvcj0ibWlkZGxlIiBmb250LXNpemU9IjEzcHgiPjx0ZXh0IHg9IjcwNS41IiB5PSIxMDguNSI+UHVibGlzaCB0bzwvdGV4dD48dGV4dCB4PSI3MDUuNSIgeT0iMTI0LjUiPiJjb29sL3RvcGljIjwvdGV4dD48L2c+PGcgZmlsbD0iI0MwNzUxRiIgZm9udC1mYW1pbHk9IkhlbHZldGljYSIgdGV4dC1hbmNob3I9Im1pZGRsZSIgZm9udC1zaXplPSIxM3B4Ij48dGV4dCB4PSI0NzEuNSIgeT0iODYuNSI+UmVjZWl2ZSBvdmVywqA8L3RleHQ+PHRleHQgeD0iNDcxLjUiIHk9IjEwMi41Ij5zaGFyZWQgYnJva2VyIGNvbm5lY3Rpb248L3RleHQ+PC9nPjxnIGZpbGw9IiNDMDc1MUYiIGZvbnQtZmFtaWx5PSJIZWx2ZXRpY2EiIHRleHQtYW5jaG9yPSJtaWRkbGUiIGZvbnQtc2l6ZT0iMTNweCI+PHRleHQgeD0iNDcyLjUiIHk9IjE4Ni41Ij5SZWNlaXZlIG92ZXI8L3RleHQ+PHRleHQgeD0iNDcyLjUiIHk9IjIwMi41Ij5kZWRpY2F0ZWQgYnJva2VyIGNvbm5lY3Rpb248L3RleHQ+PC9nPjxnIGZpbGw9IiMyQTVFNzQiIGZvbnQtZmFtaWx5PSJIZWx2ZXRpY2EiIHRleHQtYW5jaG9yPSJtaWRkbGUiIGZvbnQtc2l6ZT0iMTNweCI+PHRleHQgeD0iMjE2IiB5PSI3NSI+RmFuLW91dMKgPC90ZXh0Pjx0ZXh0IHg9IjIxNiIgeT0iOTEiPnRvIGNsaWVudHPCoDwvdGV4dD48L2c+PC9nPjwvc3ZnPg==)

</div>

<div class="title">

Figure 10. Shared subscriptions

</div>

</div>

<div class="paragraph">

MQTT.Cool receives the message over the shared broker connection
established to support the `MqttClient` instances 1, 2 and 3 (all
connected to the same broker), and also over the dedicated one, which
has been activated to allow communications to/from the `MqttClient`
instance 4. The message is finally relayed to all clients. In the case
of shared connection, instead of sending a copy of the message to each
connected client individually, the MQTT broker has delegated such heavy
task to MQTT.Cool, thus releasing its own resources to serve other
clients and dispatch other messages.

</div>

<div class="paragraph">

Lastly, before using a shared connection, take in consideration the
following constraints:

</div>

<div class="ulist">

-   QoS levels 1 and 2 are only partially supported, as will be detailed
    in the next sections.

-   As said before, the ClientId cannot be specified explicitly on the
    client side; on the contrary, it will be generated by appending a
    random string to the *clientid\_prefix* parameter to be configured
    in `mqtt_master_connector_conf.xml`, as already mentioned in
    [Section 2.1, “Static Lookup”](#static_lookup).

-   Session persistence is **NOT** supported.

-   Will Message cannot be specified explicitly on the client side, but
    only globally and for all clients sharing a connection, once again
    through the `mqtt_master_connector_conf.xml` file.

</div>

<div class="sect4">

##### Life-Cycle Events {#_life_cycle_events_2}

<div class="paragraph">

In a shared end-to-end connection, the life-cycle events relative to
`MqttClient`, MQTT channel and shared broker connection are only
partially tied together, namely:

</div>

<div class="ulist">

-   A connection request initiated by `MqttClient` implies that the
    newly created MQTT channel will be logically joined to an already
    active shared broker connection; the shared MQTT connection will be
    established only the very first time that an `MqttClient` instance
    connects to the broker.

-   A disconnection request initiated by `MqttClient`, which means
    closure of the MQTT channel, will cause only a *logical* detaching
    from the shared broker connection, which will be closed gracefully
    (that is, via an explicit `DISCONNECT` Control Packet) only the very
    last time that an `MqttClient` instance disconnects from the broker.

-   An interruption of the shared broker connection (due to any network
    issue or to problem in the MQTT broker process), will be propagated
    back to all sharing `MqttClient` instances, which in turn will
    disconnect from MQTT.Cool by closing the relative MQTT channels.

-   An interruption of the MQTT.Cool connection on the client side (due
    to any network issue or to an explicit `MQTTCoolSession` closing),
    will be managed by MQTT.Cool as a logical detaching of all the
    engaged MQTT channels from the shared broker connection, which will
    be closed gracefully only when no more MQTT channels are attached.

-   Any MQTT.Cool server failure will cause the interruption of the
    shared broker connection on the server side as well as all the
    engaged MQTT.Cool connections on the client side.

</div>

<div class="admonitionblock note">

  ---- --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  **   Any issue on the MQTT.Cool connection detected on the client side will cause the `MqttClient` instance to try a reconnection (as you will see in [Section 3.12, “Reconnecting”](#reconnecting)).
  ---- --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

</div>

</div>

</div>

</div>

<div class="sect2">

### 3.7. Specifying Connection Options {#connection_options}

<div class="paragraph">

As already mentioned before, you can specify a set of options on
connection establishment with any MQTT broker. For example, if required
by the target server, or even if you want to add a custom authentication
functionality to MQTT.Cool through a plugged Hook, you may provide
*username* and *password*:

</div>

<div class="listingblock">

<div class="content">

``` {.CodeRay .highlight}
var connectOptions = { username: 'my_mqtt_username', password: 'my_mqtt_password' };
```

</div>

</div>

<div class="admonitionblock warning">

  ---- ------------------------------------------------------------------------------------------------------------------------------------------------
  **   The credentials used to connect to MQTT brokers are **not** related to the ones which may be specified to open new sessions against MQTT.Cool.
  ---- ------------------------------------------------------------------------------------------------------------------------------------------------

</div>

<div class="paragraph">

Very important, it is generally advisable to set the proper callback
functions to handle the connection outcomes and any authorization issue
you may have:

</div>

<div class="listingblock">

<div class="content">

``` {.CodeRay .highlight}
connectOptions.onSuccess = function() {
  console.log('Connection successful');
}

connectOptions.onFailure = function(responseObject) {
  console.log('Connection failure!');
}

connectOptions.onNotAuthorized = function(responseObject) {
  console.log('Connection NOT authorized!');
}
```

</div>

</div>

<div class="paragraph">

In particular:

</div>

<div class="ulist">

-   [`onSuccess`](http://www.lightstreamer.com/api/mqtt.cool-web-client/latest/global.html#OnConnectionSuccess)
    is invoked in case of successful connection to the target MQTT
    broker; afterwards, the `MqttClient` instance switches to the
    *connected* status.

-   [`onFailure`](http://www.lightstreamer.com/api/mqtt.cool-web-client/latest/global.html#OnConnectionFailure)
    is invoked in case of any issue with either the target MQTT broker
    or the MQTT.Cool server.

-   [`onNotAuthorized`](http://www.lightstreamer.com/api/mqtt.cool-web-client/latest/global.html#OnConnectionNotAuthorized)
    is invoked in case of any authorization issue raised by the plugged
    Hook, if any (as will be shown in [Section 4.2.5, “Authorizing
    Connection”](#hook_authorizing_connection)).

</div>

<div class="paragraph">

To specify a Will Message, create and configure a `Message` instance and
add it to the options:

</div>

<div class="listingblock">

<div class="content">

``` {.CodeRay .highlight}
var myWillMessage = new Message('my_will_message');
myWillMessage.destinationName = 'my_will/topic';
connectOptions.willMessage = myWillMessage;
```

</div>

</div>

<div class="paragraph">

Upon connection, such message is stored to the target MQTT broker and
will be published to the specified Will Topic if the end-to-end
connection closes abruptly (or any other event mentioned in the MQTT
Protocol Specifications).

</div>

<div class="paragraph">

If you want to make the session persistent, you have to set the Clean
Session flag to `false`, otherwise any previous session will be
discarded upon successful connection:

</div>

<div class="listingblock">

<div class="content">

``` {.CodeRay .highlight}
connectOptions.cleanSession = false;
```

</div>

</div>

<div class="admonitionblock note">

  ---- --------------------------------------------------------------------------------------------------
  **   Will Message and Clean Session flag can only be set in the context of a **dedicated connection**
  ---- --------------------------------------------------------------------------------------------------

</div>

<div class="sect3">

#### 3.7.1. Managing Persistent Session {#_managing_persistent_session}

<div class="paragraph">

If you start a dedicated connection requiring a persistent session, its
related data are normally saved on the default local storage, which is
based on:

</div>

<div class="ulist">

-   the global `localStorage` property for web browsers

-   the local file system for Node.js runtime

</div>

<div class="paragraph">

In addition, you also have the option to supply a custom persistence
layer, by setting the `storage` connection option with an implementation
of the
[`MqttStorage`](http://www.lightstreamer.com/api/mqtt.cool-web-client/latest/MqttStorage.html)
interface:

</div>

<div class="listingblock">

<div class="content">

``` {.CodeRay .highlight}
var myCustomStorage = {

  get: function(key) { ... },

  set: function(key, value) { ... }.

  remove: function(key) { ... },

  keys: function() { ... }
}
connectOptions.storage = myCustomStorage;
```

</div>

</div>

<div class="admonitionblock note">

+-----------------------------------+-----------------------------------+
| **                                | <div class="paragraph">           |
|                                   |                                   |
|                                   | In the case of Node.js, the       |
|                                   | additional `storePath` property   |
|                                   | allows you to specify the         |
|                                   | directory which will host the     |
|                                   | files used to store the session   |
|                                   | data:                             |
|                                   |                                   |
|                                   | </div>                            |
|                                   |                                   |
|                                   | <div class="listingblock">        |
|                                   |                                   |
|                                   | <div class="content">             |
|                                   |                                   |
|                                   | ``` {.CodeRay .highlight}         |
|                                   | connectOptions.storePath = 'my/lo |
|                                   | cal/path';                        |
|                                   | ```                               |
|                                   |                                   |
|                                   | </div>                            |
|                                   |                                   |
|                                   | </div>                            |
+-----------------------------------+-----------------------------------+

</div>

</div>

<div class="sect3">

#### 3.7.2. Managing Connection Lost {#managing_connection_lost}

<div class="paragraph">

Before opening a connection, you might want to provide the
[`onConnectionLost`](http://www.lightstreamer.com/api/mqtt.cool-web-client/latest/MqttClient.html#onConnectionLost)
callback function in order to properly manage the event of an end-to end
connection lost. The callback has to be set on the `MqttClient`
instance:

</div>

<div class="listingblock">

<div class="content">

``` {.CodeRay .highlight}
...
mqttClient.onConnectionLost = function(responseObject) {
  console.log('The Connection has been lost, due to ' + responseObject.errorCode);
};
```

</div>

</div>

<div class="paragraph">

An end-to-end connection could be lost for one of the following reasons:

</div>

<div class="ulist">

-   A regular disconnection initiated through invocation of the
    [`disconnect`](http://www.lightstreamer.com/api/mqtt.cool-web-client/latest/MqttClient.html#disconnect)
    method.

-   A disconnection from MQTT.Cool triggered through invocation of the
    [`MQTTCoolSession.close`](http://www.lightstreamer.com/api/mqtt.cool-web-client/latest/MQTTCoolSession.html#close)
    method (on the same `MQTTCoolSession` instance which originated the
    `MqttClient` object).

-   An interruption of the broker connection.

-   Stop of the reconnection attempts which follow an interruption of
    the MQTT.Cool connection, as will be discussed in [Section 3.12.2,
    “Starting to Reconnect”](#starting_to_reconnect).

</div>

<div class="paragraph">

Each cause comes with its own error code and description, which are
embedded in the `responseObject` passed to the callback.

</div>

<div class="paragraph">

After losing the connection, the `MqttClient` instance switches to the
*disconnected* status, from which it would be possible to start a new
connection.

</div>

</div>

</div>

<div class="sect2">

### 3.8. The Message Class {#_the_message_class}

<div class="paragraph">

The
[`Message`](http://www.lightstreamer.com/api/mqtt.cool-web-client/latest/Message.html)
class is a wrapper of the `PUBLISH` Control Packet, which lets you send
and receive *Application Messages* to and from any MQTT broker through
an end-to-end connection.

</div>

<div class="paragraph">

Generally, you need to explicitly make an instance of `Message` class
when you have to publish messages to the broker; on the contrary, when
receiving a message from a subscription, the library provides you with
an already built instance.

</div>

<div class="paragraph">

To prepare a new `Message` object, simply invoke the constructor passing
a payload and set the required properties:

</div>

<div class="listingblock">

<div class="content">

``` {.CodeRay .highlight}
// Create a message starting from a string object
var message = new Message('A message');

// Set the target topic
message.destinationName = 'cool/topic';

// Set the Quality of Service
message.qos = 1;

// Set the retained flag
message.retained = true;
...
// Get the current duplicate flag
var dup = message.duplicate;
```

</div>

</div>

<div class="admonitionblock tip">

  ---- -----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  **   `destinationName`, `qos` and `retained` are defined as read-write properties, while in contrast `duplicate` is a **read-only** property as it can only be set on messages received from the broker.
  ---- -----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

</div>

<div class="paragraph">

Besides string objects, you are free to supply even binary payloads,
which can be expressed as `ArrayBuffer` or `TypedArray` objects:

</div>

<div class="listingblock">

<div class="content">

``` {.CodeRay .highlight}
// Create a message starting from an Uint8Array
var message = new Message(new Uint8Array([13, 73]));

// Create a message starting from a Float64Array
var message2 = new Message(new Float64Array([0.34, 0.122]));

// Create a message starting from an ArrayBuffer
var buffer = new ArrayBuffer(4);
var uint8Array = new Uint8Array(buffer);
uint8Array[0] = 1;
uint8Array[1] = 2;
uint8Array[2] = 3;
uint8Array[3] = 4;
var message3 = new Message(buffer);
```

</div>

</div>

<div class="paragraph">

String and binary payloads can be read by accessing their respective
read-only properties:

</div>

<div class="listingblock">

<div class="content">

``` {.CodeRay .highlight}
function onReceiveMessage(message) {
  // Get the payload as a string
  var strPayload = message.payloadString;
  ...

  // Get the payload as an ArrayBuffer
  var binaryPayload = message.payloadBytes;
  ...

});
```

</div>

</div>

<div class="paragraph">

Of course, you could get a string from a source binary payload or
vice-versa, but you might want to access the right property based on the
original content, in order to avoid annoying conversions.

</div>

</div>

<div class="sect2">

### 3.9. Publishing {#_publishing}

<div class="paragraph">

To publish messages to the connected MQTT broker, you have to use the
[`send`](http://www.lightstreamer.com/api/mqtt.cool-web-client/latest/MqttClient.html#send)
method, which can be used in two different forms based on the number and
the type of the provided arguments:

</div>

<div class="ulist">

-   *Single Argument Form*: the `send` method takes just one argument,
    which is the `Message` instance to be published. For example:

    <div class="listingblock">

    <div class="content">

    ``` {.CodeRay .highlight}
    ...
    // Prepare the Message instance
    var msg = new Message('My Message!')
    msg.destinationName = 'my/topic';
    msg.qos = 1;
    msg.retained = false;

    // Send the prepared message
    client.send(msg);
    ```

    </div>

    </div>

-   *Multiple Arguments Form*: the `send` method takes up to four
    arguments, which specify the details of the message to be published.
    In this case, the arguments which are not explicitly provided will
    assume default values (see the [API
    reference](http://www.lightstreamer.com/api/mqtt.cool-web-client/latest/MqttClient.html#send)).
    For example:

    <div class="listingblock">

    <div class="content">

    ``` {.CodeRay .highlight}
    // Send message by specifying topic and payload
    client.send('my/cool/topic1', 'My Message!');

    // Send message by specifying topic, payload and qos
    client.send('my/cool/topic2', 'My Message!', 1);

    // Send message by specifying topic, payload, qos and retained flag
    client.send('my/cool/topic3', 'My Message!', 1, true);
    ```

    </div>

    </div>

</div>

<div class="admonitionblock warning">

  ---- ------------------------------------------------------------------------------------------------------------------------------------
  **   You cannot provide arguments in a mixed form (for example, passing a `Message` instance as first parameter and a topic as second).
  ---- ------------------------------------------------------------------------------------------------------------------------------------

</div>

<div class="sect3">

#### 3.9.1. Message Delivery Notification {#message_delivery_notifications}

<div class="paragraph">

If you want to be notified about the outcome of a message delivery, all
you need is to set on the `MqttClient` instance a pair of callback
functions.

</div>

<div class="paragraph">

In particular,
[`onMessageNotAuthorized`](http://www.lightstreamer.com/api/mqtt.cool-web-client/latest/MqttClient.html#onMessageNotAuthorized)
will be triggered in case of any authorization issue raised by the
plugged Hook once the message is received by MQTT.Cool (as will be
described in [Section 4.2.6, “Authorizing Message
Publishing”](#hook_authorizing_publishing)):

</div>

<div class="listingblock">

<div class="content">

``` {.CodeRay .highlight}
...
mqttClient.onMessageNotAuthorized = function(message, responseObject) {
  console.log('Publishing of message targeted to topic ' + message.destinationName +
    ' NOT authorized!');

  // Check if responseObject has been actually provided
  if (responseObject) {
    var code = responseObject.errorCode;
    var msg =  responseObject.errorMessage
    console.log('code: ' + code + ', message: ' + msg);
  }
};
```

</div>

</div>

<div class="paragraph">

while
[`onMessageDelivered`](http://www.lightstreamer.com/api/mqtt.cool-web-client/latest/MqttClient.html#onMessageDelivered)
will be invoked once the delivery process completes:

</div>

<div class="listingblock">

<div class="content">

``` {.CodeRay .highlight}
...
mqttClient.onMessageDelivered = function(message) {
  console.log('The Message has been delivered to topic ' + message.destinationName);
};
```

</div>

</div>

<div class="paragraph">

In this latter case, successful completion of the delivery process
depends on several factors:

</div>

<div class="ulist">

-   The QoS level used to deliver the message.

-   The current end-to-end connection type (shared or dedicated).

-   Whether the session is persistent, which is allowed only in the case
    of a dedicated connection.

</div>

<div class="sect4">

##### QoS 0 Message {#_qos_0_message}

<div class="paragraph">

`onMessageDelivered` will be triggered once the message has been
delivered to the underlying MQTT channel (irrespective of the connection
type, shared or dedicated), and before any possible authorization issue
which could be raised when the message is actually received by
MQTT.Cool.

</div>

</div>

<div class="sect4">

##### QoS &gt; 0 Message {#_qos_0_message_2}

<div class="paragraph">

`onMessageDelivered` will be invoked on the basis of the end-to-end
connection type, as follows:

</div>

<div class="ulist">

-   For a shared connection and a dedicated connection **without**
    session persistence, the invocation occurs when MQTT.Cool sends back
    the acknowledgment that the flow of the Control Packets exchanged on
    the server side and relative to the [delivery
    protocol](http://docs.oasis-open.org/mqtt/mqtt/v3.1.1/os/mqtt-v3.1.1-os.html#_Toc398718099)
    for the specified QoS level, has been completed.

-   For a dedicated connection **with** session persistence, the
    invocation occurs in accordance with the flow of the Control Packets
    exchanged between `MqttClient` and the MQTT broker and relative to
    the aforementioned delivery protocol. More specifically:

    <div class="ulist">

    -   For QoS 1 message, upon receiving the `PUBACK` Control Packet,
        the callback is invoked and then the message is removed from the
        local storage.

    -   For QoS 2 message, upon receiving the `PUBREC` Control Packet,
        the message state is updated on the local storage and then the
        `PUBREL` Control Packet is sent back; upon receiving the
        `PUBCOMP` Control Packet, the callback is invoked and then the
        message is finally removed from the local storage.

    </div>

</div>

<div class="admonitionblock note">

  ---- -----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  **   The callback will be never invoked in case of any authorization issue raised by the plugged Hook. Under this circumstance, the message is also removed from the local storage if session persistence is active.
  ---- -----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

</div>

</div>

</div>

</div>

<div class="sect2">

### 3.10. Subscribing {#_subscribing}

<div class="paragraph">

To start receiving messages from the connected MQTT broker, you first
have to provide the `MqttClient` instance with the
[`onMessageArrived`](http://www.lightstreamer.com/api/mqtt.cool-web-client/latest/MqttClient.html#onMessageArrived)
callback function, which will be invoked when messages arrive. Then, you
must subscribe to the MQTT topics of interest by using the
[`subscribe`](http://www.lightstreamer.com/api/mqtt.cool-web-client/latest/MqttClient.html#subscribe)
method, specifying a *topic filter* and an optional set of subscribe
options:

</div>

<div class="listingblock">

<div class="content">

``` {.CodeRay .highlight}
...
// Set the callback function for receiving messages
mqttClient.onMessageArrived = function(message) {
  var topic = message.destinationName;
  var qos = message.qos;
  console.log('Received message from topic ' + topic + ' with QoS ' + qos);
};

// Prepare the set of subscription options
var subscribeOptions = { ... };

// Request the subscription to the MQTT broker
mqttClient.subscribe('my/cool/topic', subscribeOptions);
...
```

</div>

</div>

<div class="paragraph">

Let’s now analyze in detail the subscription process.

</div>

<div class="sect3">

#### 3.10.1. Topic Filter {#_topic_filter}

<div class="paragraph">

As allowed by the MQTT Protocol Specifications, the provided topic
filter can also contain special
[wildcard](http://docs.oasis-open.org/mqtt/mqtt/v3.1.1/os/mqtt-v3.1.1-os.html#_Toc398718107)
characters so that you can subscribe to multiple topics at once. In
particular, you can use *Multi-level* wildcard, *Single level* wildcard,
or even mix them:

</div>

<div class="listingblock">

<div class="content">

``` {.CodeRay .highlight}
// Subscribe to topic filter with Multi-level wildcard
mqttClient.subscribe('my/#/topic', subscribeOptions);

// Subscribe to topic filter with Single level wildcard
mqttClient.subscribe('my/cool/+', subscribeOptions);

// Mix Multi-level and Single Level wildcard in the same topic filter
mqttClient.subscribe('my/+/topic/#', subscribeOptions);
```

</div>

</div>

</div>

<div class="sect3">

#### 3.10.2. Subscribe Options {#subscribe_options}

<div class="paragraph">

By means of subscribe options, you can specify several parameters which
allow you to govern how the subscription has to be requested to the
broker.

</div>

<div class="sect4">

##### Requested QoS {#_requested_qos}

<div class="paragraph">

Through the `qos` property you can request the maximum *Quality Of
Service* with which the target MQTT broker is allowed to send messages:

</div>

<div class="listingblock">

<div class="content">

``` {.CodeRay .highlight}
...
// Set the requested QoS value
var subscribeOptions = { qos: 1 };
```

</div>

</div>

</div>

<div class="sect4">

##### Callbacks {#_callbacks}

<div class="paragraph">

To be notified about the outcome of the subscription request, you might
want to provide two callback functions:

</div>

<div class="ulist">

-   [`onSuccess`](http://www.lightstreamer.com/api/mqtt.cool-web-client/latest/global.html#OnSubscriptionSuccess),
    which will be triggered on successful acknowledgment of the request,
    also notifying of the maximum QoS level granted by the broker.

-   [`onFailure`](http://www.lightstreamer.com/api/mqtt.cool-web-client/latest/global.html#OnSubscriptionFailure),
    which will be invoked in case of request failure (with relative
    error code).

</div>

<div class="paragraph">

Below an example:

</div>

<div class="listingblock">

<div class="content">

``` {.CodeRay .highlight}
...
subscribeOptions.onSuccess = function(grantedQoS) {
  console.log('Acknowledged subscription with granted QoS: ' + grantedQoS);
};

subscribeOptions.oFailure = function(responseObject) {
  console.log('Subscription request failed with error code: ' + responseObject.errorCode);
};
```

</div>

</div>

<div class="paragraph">

In addition, by setting the
[`onSubscriptionNotAuthorized`](http://www.lightstreamer.com/api/mqtt.cool-web-client/latest/global.html#OnSubscriptionNotAuthorized)
callback function, you can also catch any authorization issue which
could be raised by the plugged Hook (as you will see in [Section 4.2.7,
“Authorizing Subscription”](#hook_authorizing_subscription)):

</div>

<div class="listingblock">

<div class="content">

``` {.CodeRay .highlight}
...
subscribeOptions.onSubscriptionNotAuthorized = function(responseObject) {
  console.log('Subscription NOT authorized!');

  // Check if responseObject has been actually provided
  if (responseObject) {
    var code = responseObject.errorCode;
    var message = responseObject.errorMessage;
    console.log('code: ' + code + ', message: ' + msg);
  }

};
```

</div>

</div>

</div>

<div class="sect4">

##### Frequency Management {#_frequency_management}

<div class="paragraph">

In the case of a shared connection, you also have the opportunity to
specify the maximum update frequency at which MQTT.Cool can route
messages from the target MQTT broker to the client:

</div>

<div class="listingblock">

<div class="content">

``` {.CodeRay .highlight}
...
subscribeOptions.maxUpdateFrequency = 100;
```

</div>

</div>

<div class="paragraph">

The rate has to be expressed in *message/sec* and can be applied only
for subscriptions made with QoS 0.

</div>

<div class="paragraph">

By leveraging this powerful feature, which is based on the native
potentialities of the underlying Lightstreamer technology, you can take
advantage of the optimized delivery employed by the Lightstreamer
Kernel, which is able to allocate the desired frequency for each
subscription requested by each client, also guaranteeing to never exceed
the demanded max frequency.

</div>

<div class="paragraph">

You can dive deeper into this and other basic concepts by having a look
at the [General
Concepts](http://www.lightstreamer.com/docs/base/General%20Concepts.pdf)
document from the Lightstreamer web site.

</div>

</div>

</div>

<div class="sect3">

#### 3.10.3. Message Arriving Notification {#_message_arriving_notification}

<div class="paragraph">

A message sent from the MQTT broker reaches `MqttClient` through the
mediation of MQTT.Cool; once arrived, the invocation of
`onMessageArrived` is based on the following factors, similarly to what
happens for `onMessageDelivered`:

</div>

<div class="ulist">

-   The QoS level at which the MQTT broker sends the message.

-   The current end-to-end connection type (shared or dedicated).

-   Whether the session is persistent, which is allowed only in the case
    of a dedicated connection.

</div>

<div class="paragraph">

In particular:

</div>

<div class="ulist">

-   For a shared connection and a dedicated connection **without**
    session persistence, the callback is triggered when MQTT.Cool
    forwards the message to `MqttClient` as soon as the delivery of the
    Control Packets exchanged on the server side and relative to the
    [delivery
    protocol](http://docs.oasis-open.org/mqtt/mqtt/v3.1.1/os/mqtt-v3.1.1-os.html#_Toc398718099)
    for the specified QoS level, has been completed.

-   For a dedicated connection **with** session persistence,
    `onMessageArrived` is called in accordance with the flow of the
    Control Packets exchanged between `MqttClient` and the MQTT broker
    and relative to the aforementioned delivery protocol. More
    specifically:

    <div class="ulist">

    -   Upon receiving a QoS 0 message, the callback is invoked
        immediately without any further elaboration.

    -   Upon receiving a QoS 1 message, the `PUBACK` Control Packet is
        sent back and then the callback is invoked.

    -   Upon receiving a QoS 2 message, it is stored immediately and
        then the `PUBREC` Control Packet is sent back; upon receiving
        the `PUBREL` Control Packet, the message is finally removed from
        the local storage, the callback is invoked and then the
        `PUBCOMP` Control Packet is sent back.

    </div>

</div>

<div class="sect4">

##### QoS Downgrading {#_qos_downgrading}

<div class="paragraph">

As already stated, for a shared connection the same message is forwarded
to all the other `MqttClient` instances that share the same broker
connection and have subscribed to the same topic filter, even specifying
a different QoS level. As consequence of this, it could be possible that
the `qos` value of the received `Message` instance gets downgraded from
the value actually granted by the MQTT broker, because the sole existing
subscription on the server side has been submitted with the maximum QoS
level among the ones of the shared subscriptions requested by the
clients.

</div>

</div>

</div>

</div>

<div class="sect2">

### 3.11. Unsubscribing

<div class="paragraph">

To stop receiving messages from previous subscribed topic(s), simply
call the
[`unsubscribe`](http://www.lightstreamer.com/api/mqtt.cool-web-client/latest/MqttClient.html#unsubscribe)
method passing the topic filter to unsubscribe from and a set of
optional parameters:

</div>

<div class="listingblock">

<div class="content">

``` {.CodeRay .highlight}
...
var unsubscribeOptions = {

  onSuccess: function() {
    console.log('Successfully unsubscribed');
  },

  onFailure: function() {
    console.log('Successfully unsubscribed');

  }
};
mqttClient.unsubscribe('my/cool/topic', unsubscribeOptions);
...
```

</div>

</div>

<div class="paragraph">

Once again, a couple of callback functions allow you to be notified
about the result of the unsubscription request, in particular:

</div>

<div class="ulist">

-   [`onSuccess`](http://www.lightstreamer.com/api/mqtt.cool-web-client/latest/global.html#OnUnsubscribeSuccess),
    will be triggered upon a successful acknowledgment of the
    unsubscription.

-   [`onFailure`](http://www.lightstreamer.com/api/mqtt.cool-web-client/latest/global.html#OnUnsubscribeFailure),
    will be invoked in case of request failure.

</div>

<div class="admonitionblock warning">

  ---- ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  **   The `onFailure` callback function is not actually employed by the current implementation of the library, as the MQTT Protocol Specifications does not define any behaviors in case of unsubscription failure. As a consequence of this, such function is only formally provided, but future use cannot be ruled out.
  ---- ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

</div>

</div>

<div class="sect2">

### 3.12. Reconnecting

<div class="paragraph">

While your `MqttClient` instance is connected, the related MQTT.Cool
connection could be interrupted, for example due to any network issue or
to problems in the MQTT.Cool server process.

</div>

<div class="paragraph">

To help you deal with this condition, the library comes with an
out-of-the-box *reconnection* feature, which allows you to try
transparently re-establishing the connection to the MQTT.Cool server,
also preserving the current *session state* of the involved `MqttClient`
instance, even when the latter was connecting without session
persistence; the state could be then resumed once the connection has
been restored.

</div>

<div class="paragraph">

Let’s elaborate a bit more on the session state.

</div>

<div class="sect3">

#### 3.12.1. The MqttClient Session State {#_the_mqttclient_session_state}

<div class="paragraph">

The session state of an `MqttClient` instance obviously depends on the
current end-to-end connection type:

</div>

<div class="ulist">

-   For a shared connection and a dedicated connection **without**
    session persistence, the session state consists of:

    <div class="olist arabic">

    1.  QoS 0 messages sent to the MQTT broker, but not yet acknowledged
        by the MQTT.Cool server.

    2.  QoS &gt; 0 messages sent to the MQTT broker, but not yet
        acknowledged by the MQTT.Cool server.

    3.  All the current active subscriptions.

    </div>

-   For a dedicated connection **with** session persistence, the session
    state is given by:

    <div class="olist arabic">

    1.  QoS 0 messages sent to the MQTT broker, but not yet acknowledged
        by the MQTT.Cool server

    2.  QoS 1 and QoS 2 messages sent to the MQTT broker, but not
        completely acknowledged.

    3.  QoS 2 messages received from the MQTT broker, but not completely
        acknowledged.

        <div class="paragraph">

        Note that the points 2 and 3 are compliant with the definition
        of *Session State* in the client as stated in the MQTT Protocol
        Specifications; instead, the point 1 goes beyond such definition
        as no recovery action is normally required to be taken for QoS 0
        messages.

        </div>

    </div>

</div>

</div>

<div class="sect3">

#### 3.12.2. Starting to Reconnect {#starting_to_reconnect}

<div class="paragraph">

By setting the
[`onReconnectionStart`](http://www.lightstreamer.com/api/mqtt.cool-web-client/latestMqttClient.html#onReconnectionStart)
callback function on the `MqttClient` instance, you will be notified
when the MQTT.Cool connection has been interrupted and an attempt to
re-establish it has started:

</div>

<div class="listingblock">

<div class="content">

``` {.CodeRay .highlight}
mqttClient.onReconnectionStart = function() {
  console.log('Starting to resume the connection...');
};
```

</div>

</div>

<div class="paragraph">

The `onReconnectionStart` callback will be invoked indefinitely until
one of the following events occurs:

</div>

<div class="ulist">

-   The MQTT.Cool connection has been restored.

-   An explicit invocation of the
    [`disconnect`](http://www.lightstreamer.com/api/mqtt.cool-web-client/latest/MqttClient.html#disconnect)
    method has been performed in the body of the provided callback, as
    follows:

    <div class="listingblock">

    <div class="content">

    ``` {.CodeRay .highlight}
    mqttClient.onReconnectionStart = function() {
      // Issue in the underlying connection, stop any reconnection attempt
      mqttClient.disconnect();
    };
    ```

    </div>

    </div>

</div>

<div class="paragraph">

which is also the recommended pattern to stop definitively any
reconnection attempt. In this case, there will not be any further
chances to resume the state of an `MqttClient` instance that is without
a persistent session.

</div>

<div class="admonitionblock warning">

  ---- -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  **   The callback is invoked only if the `MqttClient` instance was previously in the connected status: if the MQTT.Cool connection was interrupted just before `MqttClient` connects through the `connect` method, a connection failure will be immediately triggered. See the API reference relative to the [OnConnectionFailure](http://www.lightstreamer.com/api/mqtt.cool-web-client/latest/global.html#OnConnectionFailure) (the case with `errorCode=10`).
  ---- -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

</div>

</div>

<div class="sect3">

#### 3.12.3. Completing Reconnection {#_completing_reconnection}

<div class="paragraph">

As soon as the MQTT.Cool connection is restored, the `MqttClient`
instance and the MQTT.Cool server cooperate silently in order to fully
restore the whole end-to-end connection, whereupon the session state
will be resumed as follows:

</div>

<div class="ulist">

-   For a shared connection and a dedicated connection **without**
    session persistence:

    <div class="ulist">

    -   All the active subscriptions will be resubmitted silently.

    -   Sent QoS 0 messages, not yet acknowledged by the MQTT.Cool
        server, will be redelivered, although the `onMessageDelivered`
        notification will no longer take place.

    -   Sent QoS &gt; 0 messages, not yet acknowledged by the MQTT.Cool
        server, will be redelivered; in this case, the flow of
        notification will prosecute as if the messages had been sent for
        the first time, which means that `onMessageDelivered` will be
        invoked as expected.

        <div class="paragraph">

        Furthermore, message redelivery triggered on the client side
        could cause duplicates, since on the server side the same
        message may be sent and acknowledged completely before the
        end-to-end connection is interrupted: this specific condition
        represents a concern in the case of QoS 2 messages, as the MQTT
        Protocol Specifications do not allow duplicates.

        </div>

    </div>

-   For a dedicated connection **with** session persistence:

    <div class="ulist">

    -   Sent QoS 0 messages, not yet acknowledged by MQTT.Cool, will be
        redelivered, although the `onMessageDelivered` notification will
        no longer take place.

    -   Sent QoS 1 and 2 messages, not yet completely acknowledged, will
        be reprocessed as per the reached level of acknowledgment.

    -   Received QoS 2 messages, not yet completely acknowledged to the
        MQTT broker, will be reprocessed as per the reached level of
        acknowledgment.

    </div>

</div>

<div class="paragraph">

In order to be notified when the reconnection process successfully
completes, provide the `MqttClient` instance with the
[`onReconnectionComplete`](http://www.lightstreamer.com/api/mqtt.cool-web-client/latest/MqttClient.html#onReconnectionComplete)
callback, as follows:

</div>

<div class="listingblock">

<div class="content">

``` {.CodeRay .highlight}
mqttClient.onReconnectionComplete = function() {
  console.log('The connection has been successfully resumed');
};
```

</div>

</div>

</div>

</div>

<div class="sect2">

### 3.13. Disconnecting

<div class="paragraph">

To explicitly disconnect from the MQTT broker, it is only required a
straight invocation of the
[`disconnect`](http://www.lightstreamer.com/api/mqtt.cool-web-client/latest/MqttClient.html#disconnect)
method:

</div>

<div class="listingblock">

<div class="content">

``` {.CodeRay .highlight}
...
mqttClient.disconnect();
...
```

</div>

</div>

<div class="paragraph">

After sending the `DISCONNECT` Control Packet, `MqttClient` immediately
switches to the disconnected status and closes the underlying MQTT
channel, which provokes
[`onConnectionLost`](http://www.lightstreamer.com/api/mqtt.cool-web-client/latest/MqttClient.html#onConnectionLost)
to be fired (as already anticipated in [Section 3.7.2, “Managing
Connection Lost”](#managing_connection_lost)). However, the MQTT.Cool
connection remains up, as it may serve the active MQTT channels owned by
the other connected `MqttClient` objects which share the same parent
`MQTTCoolSession` instance.

</div>

<div class="admonitionblock tip">

  ---- ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  **   From the disconnected status, an `MqttClient` object is allowed to open a new connection through the [`connect`](http://www.lightstreamer.com/api/mqtt.cool-web-client/latest/MqttClient.html#connect) method.
  ---- ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

</div>

</div>

</div>

</div>

<div class="sect1">

4. The MQTT.Cool Hook {#_the_mqtt_cool_hook}
---------------------

<div class="sectionbody">

<div class="paragraph">

In this chapter, we will describe the Hook and its role in the MQTT.Cool
architecture; in addition, a developer guide will help you learn how to
make and use custom Hooks.

</div>

<div class="sect2">

### 4.1. Basics {#_basics}

<div class="paragraph">

The MQTT.Cool Hook is a custom pluggable component which provides a
powerful extension mechanism to integrate your own authentication and
authorization functionalities into the MQTT.Cool server.

</div>

<div class="paragraph">

By using the *MQTT.Cool SDK for Java Hooks* you can develop and package
your Hook, which will be then deployed into the MQTT.Cool installation;
once loaded inside the running server process, it will be able to
intercept specific events originated from the client side in order to
apply fine-grained custom authorization checks as per your own security
needs. In addition, it can also extend the default Static Lookup
mechanism provided by MQTT.Cool.

</div>

</div>

<div class="sect2">

### 4.2. Hook Development {#_hook_development}

<div class="paragraph">

The following sections will guide you through the core concepts of Hook
development.

</div>

<div class="sect3">

#### 4.2.1. Setting Up the Development Environment {#_setting_up_the_development_environment}

<div class="paragraph">

The MQTT.Cool SDK for Java Hooks provides an [open
source](https://github.com/MQTTCool/mqtt.cool-hook-java-api) API through
which you can easily develop any Hook.

</div>

<div class="paragraph">

Since the API is available from the Maven Central Repository, add the
following dependency to your `pom.xml` to set up your development
environment :

</div>

<div class="listingblock">

<div class="content">

``` {.CodeRay .highlight}
<dependency>
    <groupId>cool.mqtt.hook</groupId>
    <artifactId>mqtt.cool-hook-api</artifactId>
    <version>1.0.0/version>
</dependency>
```

</div>

</div>

<div class="admonitionblock note">

  ---- ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  **   Please note that other dependency management tools like *Gradle* or *Ivy* may be used as well. Take a look at the `<MQTT.COOL_HOME>/DOCS-SDKs/sdk_hook/README.TXT` file (also available [online](http://www.lightstreamer.com/latest/mqtt.cool/DOCS-SDKs/sdk_hook/README.TXT)) for more information.
  ---- ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

</div>

</div>

<div class="sect3">

#### 4.2.2. The MQTTCoolHook Interface {#_the_mqttcoolhook_interface}

<div class="paragraph">

Basically, an MQTT.Cool Hook is implemented through a user defined Java
class which implements the
[`MQTTCoolHook`](http://www.lightstreamer.com/api/mqtt.cool-hook-sdk/latest/cool/mqtt/hooks/MQTTCoolHook.html)
interface.

</div>

<div class="paragraph">

Such interface exposes a set of methods which may be categorized as
follows:

</div>

<div class="ulist">

-   *Authorization Requests*, which are expected to return a boolean
    value or throw an exception:

    <div class="ulist">

    -   [`canOpenSession`](http://www.lightstreamer.com/api/mqtt.cool-hook-sdk/latest/cool/mqtt/hooks/MQTTCoolHook.html#canOpenSession-java.lang.String-java.lang.String-java.lang.String-java.util.Map-java.lang.String-),
        to check the authorization for opening a new session against the
        MQTT.Cool server

    -   [`canConnect`](http://www.lightstreamer.com/api/mqtt.cool-hook-sdk/latest/cool/mqtt/hooks/MQTTCoolHook.html#-java.lang.String-java.lang.String-java.lang.String-cool.mqtt.hooks.MqttConnectOptions-),
        to check the authorization for creating a connection to a
        specified MQTT broker

    -   [`canPublish`](http://www.lightstreamer.com/api/mqtt.cool-hook-sdk/latest/cool/mqtt/hooks/MQTTCoolHook.html#canPublish-java.lang.String-java.lang.String-java.lang.String-cool.mqtt.hooks.MqttMessage-),
        to check the authorization for message publishing

    -   [`canSubscribe`](http://www.lightstreamer.com/api/mqtt.cool-hook-sdk/latest/cool/mqtt/hooks/MQTTCoolHook.html#canSubscribe-java.lang.String-java.lang.String-java.lang.String-cool.mqtt.hooks.MqttSubscription-),
        to check the authorization for subscribing to topics

    </div>

-   *Simple Notifications*, which simply inform about specific events:

    <div class="ulist">

    -   [`init`](http://www.lightstreamer.com/api/mqtt.cool-hook-sdk/latest/cool/mqtt/hooks/MQTTCoolHook.html#init-java.io.File-),
        called during the MQTT.Cool initialization

    -   [`onSessionClose`](http://www.lightstreamer.com/api/mqtt.cool-hook-sdk/latest/cool/mqtt/hooks/MQTTCoolHook.html#onSessionClose-java.lang.String-),
        called to notify that a session opened against the MQTT.Cool
        server has been closed

    -   [`onDisconnection`](http://www.lightstreamer.com/api/mqtt.cool-hook-sdk/latest/cool/mqtt/hooks/MQTTCoolHook.html#onDisconnection-java.lang.String-java.lang.String-java.lang.String-),
        called to notify that a client has been disconnected from an
        MQTT broker

    -   [`onUnsubscribe`](http://www.lightstreamer.com/api/mqtt.cool-hook-sdk/latest/cool/mqtt/hooks/MQTTCoolHook.html#onUnsubscribe-java.lang.String-java.lang.String-java.lang.String-java.lang.String-),
        called to notify that a client has been unsubscribed from a
        given topic filter

    </div>

-   *Factories*, which dynamically provide further MQTT connection
    settings:

    <div class="ulist">

    -   [`resolveAlias`](http://www.lightstreamer.com/api/mqtt.cool-hook-sdk/latest/cool/mqtt/hooks/MQTTCoolHook.html#resolveAlias-java.lang.String-),
        returns a valid broker configuration if no static entries exist
        for a given connection alias.

    </div>

</div>

<div class="paragraph">

As will be shown in the subsequent sections, you might want to supply a
specific behavior only to those methods you are actually interested in,
whereas you may provide a fake implementation for all the others.
Furthermore, the SDK includes the
[`SimpleCoolHook`](http://www.lightstreamer.com/api/mqtt.cool-hook-sdk/latest/cool/mqtt/hooks/SimpleCoolHook.html)
base class, which is a skeletal implementation of the interface meant to
be extended to make it easier to provide a full implementation of a
custom Hook.

</div>

<div class="paragraph">

The `SimpleCoolHook` class provides the following default behaviors for
each specific method category:

</div>

<div class="ulist">

-   Authorization Requests: always permit.

-   Simple Notifications: do nothing.

-   Factories: return **null**.

</div>

<div class="paragraph">

Let’s start writing a simple Hook, which will help you to grasp the core
concepts needed to implement your own extensions.

</div>

</div>

<div class="sect3">

#### 4.2.3. Notifying of Hook Initialization {#_notifying_of_hook_initialization}

<div class="paragraph">

A Hook is loaded during the MQTT.Cool initialization process. If you
need to run some setup logic, you have to override the `init` method,
which is called in that phase:

</div>

<div class="listingblock">

<div class="content">

``` {.CodeRay .highlight}
package my.cool.hook;

import java.io.File;

import cool.mqtt.hooks.HookException;
import cool.mqtt.hooks.SimpleCoolHook;

public class MyCoolHook extends SimpleCoolHook {

  @Override
  public void init(File configDir) throws HookException {
    // Put here your setup logic
  }
}
```

</div>

</div>

<div class="paragraph">

The `configDir` parameter is the `<MQTT.COOL_HOME>/mqtt_connectors`
directory, where you can put any resource you may need to initialize the
Hook (for example, like configuration files).

</div>

<div class="admonitionblock warning">

  ---- -----------------------------------------------------------------------------------------------------------------------------------------------------------------
  **   Any exception thrown from the method will cause the failure of the initialization phase and, as a consequence of this, the MQTT.Cool server process will abort.
  ---- -----------------------------------------------------------------------------------------------------------------------------------------------------------------

</div>

</div>

<div class="sect3">

#### 4.2.4. Authorizing Session Opening {#hook_authorizing_session}

<div class="paragraph">

If you want to intercept a new session started by the client (as
detailed in [Section 3.4, “The MQTT.Cool Connection
Pattern”](#connection_pattern)), you have to override the
`canOpenSession` method:

</div>

<div class="listingblock">

<div class="content">

``` {.CodeRay .highlight}
@Override
public boolean canOpenSession(String sessionId, String user, String password,
  Map clientContext, String clientPrincipal) throws HookException {

  boolean canOpen = false;

  // Put here your authorization logic
  ...

  return canOpen;
}
```

</div>

</div>

<div class="paragraph">

On the basis of the parameter values, you could apply your own security
policies to authorize the session. You could also contact an external
service (like *databases* or *LDAP* servers) to authenticate the user
who is requesting to connect to MQTT.Cool. The following example shows a
straight user/password based authentication:

</div>

<div class="listingblock">

<div class="content">

``` {.CodeRay .highlight}
@Override
public boolean canOpenSession(String sessionId, String user, String password,
  Map clientContext, String clientPrincipal) throws HookException {

  if (user == null || user.trim().isEmpty()) {
    return false;
  }

  // Lookup the password form an external service (for example, a database)
  String storedPassword = lookupPassword(user);

  if (storedPassword == null) {
    return false;
  }

  boolean authenticated = storedPassword.equals(password);

  return authenticated;
}
```

</div>

</div>

<div class="paragraph">

As you have seen in [Section 3.5, “The MQTTCoolSession
Interface”](#session_interface), the
[`onConnectionFailure`](http://www.lightstreamer.com/api/mqtt.cool-web-client/latest/MQTTCoolListener.html#onConnectionFailure)
callback is invoked in case of any authorization issue:

</div>

<div class="listingblock">

<div class="content">

``` {.CodeRay .highlight}
mqttcool.openSession('http://my.server.company:8080', 'my_cool_user', 'my_wrong_password', {

  onConnectionFailure: function(errorType, errorCode, errorMessage) {
    // errorType is 'UNAUTHORIZED_SESSION'
    // errorCode and errorMessage are undefined
    if ('UNAUTHORIZED_SESSION' == errorType) {
      console.log('Authorization issue')
    } else {
      // Other connection failure conditions
      ...
    }
  }
  ...
});
```

</div>

</div>

<div class="paragraph">

In particular, the `errorType` parameter is set to the string
`UNAUTHORIZED_SESSION`, which is the reserved value for any
authorization issue, whereas the remaining parameters are `undefined`.
This is what happens when the Hook denies the authorization to open a
new session by returning the `false` value (as in the example above).
Nevertheless, you are allowed to throw a
[`HookException`](http://www.lightstreamer.com/api/mqtt.cool-hook-sdk/latest/cool/mqtt/hooks/HookException.html)
with detailed code and message, which will be forwarded respectively as
`errorCode` and `errorMessage` parameters to the client, thus enabling
the latter to distinguish the kind of problem by looking at them.

</div>

<div class="paragraph">

More generally, from any Authorization Request method you have two
options for reporting an issue to the client:

</div>

<div class="olist arabic">

1.  Return the `false` value, which is the way to go if the client
    simply needs to know whether its request has not been authorized.

2.  Throw a `HookException` with detailed information, which is the
    suggested pattern if you want the client to undertake specific
    actions based on the reported issue.

</div>

<div class="paragraph">

The following code snippet modifies the previous example: this time a
`HookException` is thrown to signal specific failure conditions,
although a boolean value is still returned to indicate whether the
provided password matches the stored one.

</div>

<div class="listingblock">

<div class="content">

``` {.CodeRay .highlight}
@Override
public boolean canOpenSession(String sessionId, String user, String password,
  Map clientContext, String clientPrincipal) throws HookException {

  // Use errorCode 101 to signal missing username
  if (user == null || user.trim().isEmpty()) {
    throw new HookException(101, "No user provided");
  }

  // Lookup the password form an external service (for example, a database)
  String storedPassword = lookupPassword(user);

  // Use errorCode 102 to signal not existing account
  if (storedPassword == null) {
    throw new HookException(102, "User \"" + user + "\" not found");
  }

  // Return a boolean value for the validation outcome
  boolean authenticated = storedPassword.equals(password);

  return authenticated;
}
```

</div>

</div>

<div class="admonitionblock warning">

  ---- ------------------------------------------------------------
  **   `HookException` accepts only **non-negative** error codes.
  ---- ------------------------------------------------------------

</div>

<div class="paragraph">

On the client side, now you can decide how to react on the basis of the
error details, sent as specified inside the raised HookException:

</div>

<div class="listingblock">

<div class="content">

``` {.CodeRay .highlight}
mqttcool.openSession('http://my.server.company:8080', 'my_cool_user', 'my_wrong_password', {

  onConnectionFailure: function(errorType, errorCode, errorMessage) {
    // errorType is 'UNAUTHORIZED_SESSION'
    // errorCode is:
    //  - undefined in case of simple password mismatch
    //  - 101 in case of no user provided
    //  - 102 in case of no user found
    // errorMessage is provided according to errorCode
    if ('UNAUTHORIZED_SESSION' == errorType) {
      if (errorCode) {
        console.log('Authorization issue: ' + errorMessage)
        // Here the actions to be undertaken for handling authorization issues
        // reported through a HookException
        ...
      } else {
        console.log('Authentication failure')
        // Here the actions to be undertaken for handling the authentication failure
        // due to password mismatch
        ...
      }
    } else {
      // Other connection failure conditions
      ...
    }
  }

  ...
});
```

</div>

</div>

<div class="admonitionblock note">

  ---- -----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  **   As you will see for the next operations, `sessionId` is always included in the signature of all Hook methods as the first parameter (except `init` and `resolveAlias`): it will take on the meaning of **already trusted session**, hence there will be no chances that any subsequent Authorization Request or *Simple Notification* may be invoked as part of an *untrusted session*.
  ---- -----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

</div>

<div class="paragraph">

The following diagram shows the sequence of messages and events on both
the client side and the server side during the creation of a session.

</div>

<div class="imageblock" style="text-align: center">

<div class="content">

![can open
session](data:image/svg+xml;base64,PCFET0NUWVBFIHN2ZyBQVUJMSUMgIi0vL1czQy8vRFREIFNWRyAxLjEvL0VOIiAiaHR0cDovL3d3dy53My5vcmcvR3JhcGhpY3MvU1ZHLzEuMS9EVEQvc3ZnMTEuZHRkIj4KPHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHhtbG5zOnhsaW5rPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hsaW5rIiB3aWR0aD0iODQ2cHgiIGhlaWdodD0iNTYxcHgiIHZlcnNpb249IjEuMSIgc3R5bGU9ImJhY2tncm91bmQtY29sb3I6IHJnYigyNTUsIDI1NSwgMjU1KTsiPjxkZWZzLz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgwLjUsMC41KSI+PHBhdGggZD0iTSAyNTIgMjI0IEwgMzQ1Ljg4IDIyNCIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJub25lIi8+PHBhdGggZD0iTSAzNTQuODggMjI0IEwgMzQ1Ljg4IDIyOC41IEwgMzQ1Ljg4IDIxOS41IFoiIGZpbGw9IiMwMDAwMDAiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0ibm9uZSIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKDI5My41LDIwOS41KSI+PHN3aXRjaD48Zm9yZWlnbk9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6dmlzaWJsZTsiIHBvaW50ZXItZXZlbnRzPSJhbGwiIHdpZHRoPSIyMSIgaGVpZ2h0PSIxMSIgcmVxdWlyZWRGZWF0dXJlcz0iaHR0cDovL3d3dy53My5vcmcvVFIvU1ZHMTEvZmVhdHVyZSNFeHRlbnNpYmlsaXR5Ij48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDExcHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiByZ2IoMCwgMCwgMCk7IGxpbmUtaGVpZ2h0OiAxLjI7IHZlcnRpY2FsLWFsaWduOiB0b3A7IHdoaXRlLXNwYWNlOiBub3dyYXA7IHRleHQtYWxpZ246IGNlbnRlcjsiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OmlubGluZS1ibG9jazt0ZXh0LWFsaWduOmluaGVyaXQ7dGV4dC1kZWNvcmF0aW9uOmluaGVyaXQ7YmFja2dyb3VuZC1jb2xvcjojZmZmZmZmOyI+bmV3PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0Pjx0ZXh0IHg9IjExIiB5PSIxMSIgZmlsbD0iIzAwMDAwMCIgdGV4dC1hbmNob3I9Im1pZGRsZSIgZm9udC1zaXplPSIxMXB4IiBmb250LWZhbWlseT0iSGVsdmV0aWNhIj5uZXc8L3RleHQ+PC9zd2l0Y2g+PC9nPjxwYXRoIGQ9Ik0gNTMwLjMzIDQyOS42NyBMIDI1OS4yNCA0MzAiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBzdHJva2UtZGFzaGFycmF5PSIzIDMiIHBvaW50ZXItZXZlbnRzPSJub25lIi8+PHBhdGggZD0iTSAyNjcuMTEgNDI1LjQ5IEwgMjU4LjEyIDQzMCBMIDI2Ny4xMiA0MzQuNDkiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0ibm9uZSIvPjxnIGZpbGw9IiMwMDAwMDAiIGZvbnQtZmFtaWx5PSJIZWx2ZXRpY2EiIGZvbnQtc3R5bGU9Iml0YWxpYyIgdGV4dC1hbmNob3I9Im1pZGRsZSIgZm9udC1zaXplPSIxMXB4Ij48cmVjdCBmaWxsPSIjZmZmZmZmIiBzdHJva2U9Im5vbmUiIHg9IjM0NCIgeT0iNDE0IiB3aWR0aD0iMTAwIiBoZWlnaHQ9IjE0IiBzdHJva2Utd2lkdGg9IjAiLz48dGV4dCB4PSIzOTIuODMiIHk9IjQyMy4zMyI+YXV0aG9yaXphdGlvbl9pc3N1ZTwvdGV4dD48L2c+PHBhdGggZD0iTSAyNTEgMTIwIEwgNTcuMjQgMTIwIiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgc3Ryb2tlLWRhc2hhcnJheT0iMyAzIiBwb2ludGVyLWV2ZW50cz0ibm9uZSIvPjxwYXRoIGQ9Ik0gNjUuMTIgMTE1LjUgTCA1Ni4xMiAxMjAgTCA2NS4xMiAxMjQuNSIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJub25lIi8+PHBhdGggZD0iTSAyNTggOTUgTCA1MjMuODggOTUiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0ibm9uZSIvPjxwYXRoIGQ9Ik0gNTMwLjg4IDk1IEwgNTIzLjg4IDk4LjUgTCA1MjMuODggOTEuNSBaIiBmaWxsPSIjMDAwMDAwIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9Im5vbmUiLz48ZyBmaWxsPSIjMDAwMDAwIiBmb250LWZhbWlseT0iSGVsdmV0aWNhIiBmb250LXN0eWxlPSJpdGFsaWMiIHRleHQtYW5jaG9yPSJtaWRkbGUiIGZvbnQtc2l6ZT0iMTFweCI+PHJlY3QgZmlsbD0iI2ZmZmZmZiIgc3Ryb2tlPSJub25lIiB4PSIzMTQiIHk9IjgwIiB3aWR0aD0iMTY0IiBoZWlnaHQ9IjE0IiBzdHJva2Utd2lkdGg9IjAiLz48dGV4dCB4PSIzOTQuNSIgeT0iODguNSI+Y3JlYXRlX3Nlc3Npb24odXNlciwgcGFzc3dvcmQpPC90ZXh0PjwvZz48cmVjdCB4PSIwIiB5PSIwIiB3aWR0aD0iMTAwIiBoZWlnaHQ9IjQwIiBmaWxsPSIjZmZmMmNjIiBzdHJva2U9IiMwMDAwMDAiIHBvaW50ZXItZXZlbnRzPSJub25lIi8+PHBhdGggZD0iTSA1MCA0MCBMIDUwIDU2MCIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHN0cm9rZS1kYXNoYXJyYXk9IjMgMyIgcG9pbnRlci1ldmVudHM9Im5vbmUiLz48ZyBmaWxsPSIjMDAwMDAwIiBmb250LWZhbWlseT0iSGVsdmV0aWNhIiBmb250LXdlaWdodD0iYm9sZCIgdGV4dC1hbmNob3I9Im1pZGRsZSIgZm9udC1zaXplPSIxMXB4Ij48dGV4dCB4PSI0OS41IiB5PSIyNCI+OldlYiBDbGllbnQ8L3RleHQ+PC9nPjxyZWN0IHg9IjQ1IiB5PSI4MCIgd2lkdGg9IjEwIiBoZWlnaHQ9IjQwIiBmaWxsPSIjZmZmZmZmIiBzdHJva2U9IiMwMDAwMDAiIHBvaW50ZXItZXZlbnRzPSJub25lIi8+PHJlY3QgeD0iNDUiIHk9IjI2OCIgd2lkdGg9IjEwIiBoZWlnaHQ9IjgyIiBmaWxsPSIjZmZmZmZmIiBzdHJva2U9IiMwMDAwMDAiIHBvaW50ZXItZXZlbnRzPSJub25lIi8+PHJlY3QgeD0iNDUiIHk9IjQ3MiIgd2lkdGg9IjEwIiBoZWlnaHQ9IjY4IiBmaWxsPSIjZmZmZmZmIiBzdHJva2U9IiMwMDAwMDAiIHBvaW50ZXItZXZlbnRzPSJub25lIi8+PHJlY3QgeD0iNDgwIiB5PSIwIiB3aWR0aD0iMTEwIiBoZWlnaHQ9IjQwIiBmaWxsPSIjZmZmMmNjIiBzdHJva2U9IiMwMDAwMDAiIHBvaW50ZXItZXZlbnRzPSJub25lIi8+PHBhdGggZD0iTSA1MzUgNDAgTCA1MzUgNTYwIiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgc3Ryb2tlLWRhc2hhcnJheT0iMyAzIiBwb2ludGVyLWV2ZW50cz0ibm9uZSIvPjxnIGZpbGw9IiMwMDAwMDAiIGZvbnQtZmFtaWx5PSJIZWx2ZXRpY2EiIGZvbnQtd2VpZ2h0PSJib2xkIiB0ZXh0LWFuY2hvcj0ibWlkZGxlIiBmb250LXNpemU9IjExcHgiPjx0ZXh0IHg9IjUzNC41IiB5PSIyNCI+Ok1RVFQuQ29vbCBTZXJ2ZXI8L3RleHQ+PC9nPjxyZWN0IHg9IjUzMCIgeT0iOTUiIHdpZHRoPSIxMCIgaGVpZ2h0PSIzNzUiIGZpbGw9IiNmZmZmZmYiIHN0cm9rZT0iIzAwMDAwMCIgcG9pbnRlci1ldmVudHM9Im5vbmUiLz48cmVjdCB4PSI3NDUiIHk9IjAiIHdpZHRoPSIxMDAiIGhlaWdodD0iNDAiIGZpbGw9IiNmZmYyY2MiIHN0cm9rZT0iIzAwMDAwMCIgcG9pbnRlci1ldmVudHM9Im5vbmUiLz48cGF0aCBkPSJNIDc5NSA0MCBMIDc5NSA1NjAiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBzdHJva2UtZGFzaGFycmF5PSIzIDMiIHBvaW50ZXItZXZlbnRzPSJub25lIi8+PGcgZmlsbD0iIzAwMDAwMCIgZm9udC1mYW1pbHk9IkhlbHZldGljYSIgZm9udC13ZWlnaHQ9ImJvbGQiIHRleHQtYW5jaG9yPSJtaWRkbGUiIGZvbnQtc2l6ZT0iMTFweCI+PHRleHQgeD0iNzk0LjUiIHk9IjI0Ij46SG9vazwvdGV4dD48L2c+PHJlY3QgeD0iNzkwIiB5PSIxMDYiIHdpZHRoPSIxMCIgaGVpZ2h0PSIzOSIgZmlsbD0iI2ZmZmZmZiIgc3Ryb2tlPSIjMDAwMDAwIiBwb2ludGVyLWV2ZW50cz0ibm9uZSIvPjxwYXRoIGQ9Ik0gNTQwIDEwNiBMIDc4My44OCAxMDYiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0ibm9uZSIvPjxwYXRoIGQ9Ik0gNzkwLjg4IDEwNiBMIDc4My44OCAxMDkuNSBMIDc4My44OCAxMDIuNSBaIiBmaWxsPSIjMDAwMDAwIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9Im5vbmUiLz48ZyBmaWxsPSIjMDAwMDAwIiBmb250LWZhbWlseT0iSGVsdmV0aWNhIiB0ZXh0LWFuY2hvcj0ibWlkZGxlIiBmb250LXNpemU9IjExcHgiPjxyZWN0IGZpbGw9IiNmZmZmZmYiIHN0cm9rZT0ibm9uZSIgeD0iNTY5IiB5PSI5MSIgd2lkdGg9IjE5NiIgaGVpZ2h0PSIxNCIgc3Ryb2tlLXdpZHRoPSIwIi8+PHRleHQgeD0iNjY1LjUiIHk9Ijk5LjUiPmNhbk9wZW5TZXNzaW9uKHVzZXIsIHRva2VuLCBjb250ZXh0KTwvdGV4dD48L2c+PHJlY3QgeD0iMjAyIiB5PSIwIiB3aWR0aD0iMTAwIiBoZWlnaHQ9IjQwIiBmaWxsPSIjZmZmMmNjIiBzdHJva2U9IiMwMDAwMDAiIHBvaW50ZXItZXZlbnRzPSJub25lIi8+PHBhdGggZD0iTSAyNTIgNDAgTCAyNTIgNTYwIiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgc3Ryb2tlLWRhc2hhcnJheT0iMyAzIiBwb2ludGVyLWV2ZW50cz0ibm9uZSIvPjxnIGZpbGw9IiMwMDAwMDAiIGZvbnQtZmFtaWx5PSJIZWx2ZXRpY2EiIGZvbnQtd2VpZ2h0PSJib2xkIiB0ZXh0LWFuY2hvcj0ibWlkZGxlIiBmb250LXNpemU9IjExcHgiPjx0ZXh0IHg9IjI1MS41IiB5PSIyNCI+Ok1RVFRDb29sPC90ZXh0PjwvZz48cmVjdCB4PSIyNDciIHk9IjE4NyIgd2lkdGg9IjEwIiBoZWlnaHQ9IjgwIiBmaWxsPSIjZmZmZmZmIiBzdHJva2U9IiMwMDAwMDAiIHBvaW50ZXItZXZlbnRzPSJub25lIi8+PHJlY3QgeD0iMjQ3IiB5PSI5MCIgd2lkdGg9IjEwIiBoZWlnaHQ9IjMwIiBmaWxsPSIjZmZmZmZmIiBzdHJva2U9IiMwMDAwMDAiIHBvaW50ZXItZXZlbnRzPSJub25lIi8+PHJlY3QgeD0iMjQ3IiB5PSI0MzAiIHdpZHRoPSIxMCIgaGVpZ2h0PSI0MSIgZmlsbD0iI2ZmZmZmZiIgc3Ryb2tlPSIjMDAwMDAwIiBwb2ludGVyLWV2ZW50cz0ibm9uZSIvPjxwYXRoIGQ9Ik0gNTUgOTAgTCAxMjUgOTAgUSAxMzUgOTAgMTQ1IDkwIEwgMjM4Ljg4IDkwIiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9Im5vbmUiLz48cGF0aCBkPSJNIDI0NS44OCA5MCBMIDIzOC44OCA5My41IEwgMjM4Ljg4IDg2LjUgWiIgZmlsbD0iIzAwMDAwMCIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJub25lIi8+PGcgZmlsbD0iIzAwMDAwMCIgZm9udC1mYW1pbHk9IkhlbHZldGljYSIgdGV4dC1hbmNob3I9Im1pZGRsZSIgZm9udC1zaXplPSIxMXB4Ij48dGV4dCB4PSIxNTAuNSIgeT0iODMuNSI+Y29ubmVjdChhZGRyZXNzLCB1c2VyLCBwYXNzd29yZCk8L3RleHQ+PC9nPjxwYXRoIGQ9Ik0gNzk2IDE0NSBMIDU0Mi4yNCAxNDUiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBzdHJva2UtZGFzaGFycmF5PSIzIDMiIHBvaW50ZXItZXZlbnRzPSJub25lIi8+PHBhdGggZD0iTSA1NTAuMTIgMTQwLjUgTCA1NDEuMTIgMTQ1IEwgNTUwLjEyIDE0OS41IiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9Im5vbmUiLz48ZyBmaWxsPSIjMDAwMDAwIiBmb250LWZhbWlseT0iSGVsdmV0aWNhIiB0ZXh0LWFuY2hvcj0ibWlkZGxlIiBmb250LXNpemU9IjExcHgiPjxyZWN0IGZpbGw9IiNmZmZmZmYiIHN0cm9rZT0ibm9uZSIgeD0iNTU1IiB5PSIxMzAiIHdpZHRoPSIyMjciIGhlaWdodD0iMTQiIHN0cm9rZS13aWR0aD0iMCIvPjx0ZXh0IHg9IjY2Ny41IiB5PSIxMzguNSI+cmV0dXJuIFRydWUgb3IgRmFsc2Ugb3IgdGhyb3cgSG9va0V4Y2VwdGlvbjwvdGV4dD48L2c+PHJlY3QgeD0iMzU2IiB5PSIyMTkiIHdpZHRoPSIxMDkiIGhlaWdodD0iNDAiIGZpbGw9IiNmZmYyY2MiIHN0cm9rZT0iIzAwMDAwMCIgcG9pbnRlci1ldmVudHM9Im5vbmUiLz48cGF0aCBkPSJNIDQxMC41IDI1OSBMIDQxMC41IDM5MCIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHN0cm9rZS1kYXNoYXJyYXk9IjMgMyIgcG9pbnRlci1ldmVudHM9Im5vbmUiLz48ZyBmaWxsPSIjMDAwMDAwIiBmb250LWZhbWlseT0iSGVsdmV0aWNhIiBmb250LXdlaWdodD0iYm9sZCIgdGV4dC1hbmNob3I9Im1pZGRsZSIgZm9udC1zaXplPSIxMXB4Ij48dGV4dCB4PSI0MTAiIHk9IjI0MyI+Ok1RVFRDb29sU2Vzc2lvbjwvdGV4dD48L2c+PHJlY3QgeD0iNDA2IiB5PSIzNDkiIHdpZHRoPSIxMCIgaGVpZ2h0PSIzMCIgZmlsbD0iI2ZmZmZmZiIgc3Ryb2tlPSIjMDAwMDAwIiBwb2ludGVyLWV2ZW50cz0ibm9uZSIvPjxwYXRoIGQ9Ik0gNTMwIDE4NyBMIDI1NS4yNCAxODciIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBzdHJva2UtZGFzaGFycmF5PSIzIDMiIHBvaW50ZXItZXZlbnRzPSJub25lIi8+PHBhdGggZD0iTSAyNjMuMTIgMTgyLjUgTCAyNTQuMTIgMTg3IEwgMjYzLjEyIDE5MS41IiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9Im5vbmUiLz48ZyBmaWxsPSIjMDAwMDAwIiBmb250LWZhbWlseT0iSGVsdmV0aWNhIiBmb250LXN0eWxlPSJpdGFsaWMiIHRleHQtYW5jaG9yPSJtaWRkbGUiIGZvbnQtc2l6ZT0iMTFweCI+PHJlY3QgZmlsbD0iI2ZmZmZmZiIgc3Ryb2tlPSJub25lIiB4PSIzNDkiIHk9IjE3MiIgd2lkdGg9Ijg1IiBoZWlnaHQ9IjE0IiBzdHJva2Utd2lkdGg9IjAiLz48dGV4dCB4PSIzOTAuNSIgeT0iMTgwLjUiPnNlc3Npb25fY3JlYXRlZDwvdGV4dD48L2c+PHBhdGggZD0iTSAyNDggMjY3IEwgNjAuMTIgMjY3IiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9Im5vbmUiLz48cGF0aCBkPSJNIDUzLjEyIDI2NyBMIDYwLjEyIDI2My41IEwgNjAuMTIgMjcwLjUgWiIgZmlsbD0iIzAwMDAwMCIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJub25lIi8+PGcgZmlsbD0iIzAwMDAwMCIgZm9udC1mYW1pbHk9IkhlbHZldGljYSIgdGV4dC1hbmNob3I9Im1pZGRsZSIgZm9udC1zaXplPSIxMXB4Ij48cmVjdCBmaWxsPSIjZmZmZmZmIiBzdHJva2U9Im5vbmUiIHg9IjkzIiB5PSIyNTIiIHdpZHRoPSIxMTUiIGhlaWdodD0iMTQiIHN0cm9rZS13aWR0aD0iMCIvPjx0ZXh0IHg9IjE0OS41IiB5PSIyNjAuNSI+b25Db25uZWN0aW9uU3VjY2VzczwvdGV4dD48L2c+PHBhdGggZD0iTSA1NSAzNDkgTCAzOTcuODggMzQ5IiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9Im5vbmUiLz48cGF0aCBkPSJNIDQwNC44OCAzNDkgTCAzOTcuODggMzUyLjUgTCAzOTcuODggMzQ1LjUgWiIgZmlsbD0iIzAwMDAwMCIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJub25lIi8+PHBhdGggZD0iTSAyNTEgNDcxIEwgNjMuMTIgNDcxLjk2IiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9Im5vbmUiLz48cGF0aCBkPSJNIDU2LjEyIDQ3MS45OSBMIDYzLjEgNDY4LjQ2IEwgNjMuMTQgNDc1LjQ2IFoiIGZpbGw9IiMwMDAwMDAiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0ibm9uZSIvPjxnIGZpbGw9IiMwMDAwMDAiIGZvbnQtZmFtaWx5PSJIZWx2ZXRpY2EiIHRleHQtYW5jaG9yPSJtaWRkbGUiIGZvbnQtc2l6ZT0iMTFweCI+PHJlY3QgZmlsbD0iI2ZmZmZmZiIgc3Ryb2tlPSJub25lIiB4PSIxMDAiIHk9IjQ1NiIgd2lkdGg9IjEwNyIgaGVpZ2h0PSIxNCIgc3Ryb2tlLXdpZHRoPSIwIi8+PHRleHQgeD0iMTUyLjUiIHk9IjQ2NSI+b25Db25uZWN0aW9uRmFpbHVyZTwvdGV4dD48L2c+PHBhdGggZD0iTSAxNSAzOTQgTCA4MTAgMzk0IiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS13aWR0aD0iMiIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBzdHJva2UtZGFzaGFycmF5PSI2IDYiIHBvaW50ZXItZXZlbnRzPSJub25lIi8+PHBhdGggZD0iTSAxNSAxNjYgTCA3NSAxNjYgTCA3NSAxODEgTCA2NSAxOTYgTCAxNSAxOTYgWiIgZmlsbD0iIzMzZmZmZiIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2Utd2lkdGg9IjIiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9Im5vbmUiLz48cGF0aCBkPSJNIDc1IDE2NiBMIDgxMSAxNjYgTCA4MTEgNTQ2IEwgMTUgNTQ2IEwgMTUgMTk2IiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS13aWR0aD0iMiIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0ibm9uZSIvPjxnIGZpbGw9IiMwMDAwMDAiIGZvbnQtZmFtaWx5PSJIZWx2ZXRpY2EiIHRleHQtYW5jaG9yPSJtaWRkbGUiIGZvbnQtc2l6ZT0iMTFweCI+PHRleHQgeD0iNDUuNSIgeT0iMTg1Ij5hbHQ8L3RleHQ+PC9nPjxnIGZpbGw9IiMwMDAwMDAiIGZvbnQtZmFtaWx5PSJIZWx2ZXRpY2EiIGZvbnQtd2VpZ2h0PSJib2xkIiBmb250LXNpemU9IjExcHgiPjx0ZXh0IHg9Ijc2LjUiIHk9IjIwNyI+W0hvb2sgcmV0dXJucyBUcnVlXTwvdGV4dD48L2c+PGcgZmlsbD0iIzAwMDAwMCIgZm9udC1mYW1pbHk9IkhlbHZldGljYSIgZm9udC13ZWlnaHQ9ImJvbGQiIGZvbnQtc2l6ZT0iMTFweCI+PHRleHQgeD0iNzYuNSIgeT0iNDE2LjUiPltIb29rIHJldHVybnMgRmFsc2U8L3RleHQ+PHRleHQgeD0iNzYuNSIgeT0iNDI5LjUiPm9ywqB0aHJvdyBIb29rRXhjZXB0aW9uXTwvdGV4dD48L2c+PHBhdGggZD0iTSAxMDAgMjgzIEwgMzMxIDI4MyBMIDM0NSAyOTcgTCAzNDUgMzE1IEwgMTAwIDMxNSBMIDEwMCAyODMgWiIgZmlsbD0iI2Y1ZjVmNSIgc3Ryb2tlPSIjNjY2NjY2IiBzdHJva2Utd2lkdGg9IjIiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9Im5vbmUiLz48cGF0aCBkPSJNIDMzMSAyODMgTCAzMzEgMjk3IEwgMzQ1IDI5NyIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjNjY2NjY2IiBzdHJva2Utd2lkdGg9IjIiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9Im5vbmUiLz48ZyBmaWxsPSIjMDAwMDAwIiBmb250LWZhbWlseT0iSGVsdmV0aWNhIiBmb250LXNpemU9IjExcHgiPjx0ZXh0IHg9IjEwMi41IiB5PSIyOTQuNSI+VGhlIGNsaWVudCBjYW4gdXNlIHRoZSBzZXNzaW9uIGZyb20gbm93IG9uPC90ZXh0PjwvZz48cGF0aCBkPSJNIDIyMS4wOSAzMTUgTCAyMTggMzUwIiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgc3Ryb2tlLWRhc2hhcnJheT0iMyAzIiBwb2ludGVyLWV2ZW50cz0ibm9uZSIvPjwvZz48L3N2Zz4=)

</div>

<div class="title">

Figure 11. Sequence diagram for session opening

</div>

</div>

</div>

<div class="sect3">

#### 4.2.5. Authorizing Connection {#hook_authorizing_connection}

<div class="paragraph">

As shown in [Section 3.4, “The MQTT.Cool Connection
Pattern”](#connection_pattern), after having established a connection to
MQTT.Cool, a client might want to connect to a specific MQTT broker. By
overriding the `canConnect` method, you can intercept and authorize the
connection request:

</div>

<div class="listingblock">

<div class="content">

``` {.CodeRay .highlight}
@Override
public boolean canConnect(String sessionId, String clientId, String brokerAddress,
  MqttConnectOptions connectOptions) throws HookException {

  boolean canConnect = false;

  // Put here your authorization logic
  ...

  return canConnect;
}
```

</div>

</div>

<div class="paragraph">

For example, you could check the credentials (provided in the connection
options) before being passed to the broker, thus enabling you to extend
the latter with a further layer of authentication logic if the native
one does not fully satisfy your security needs (or even in the case the
broker does not implement any authentication itself).

</div>

<div class="admonitionblock note">

  ---- ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  **   In the case of shared connection, although the physical MQTT connection between the MQTT.Cool server and the target MQTT broker is realized only the very first time that a client requests to connect, the `canConnect` method is invoked on each connection request issued by every *joining* client.
  ---- ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

</div>

<div class="paragraph">

The following code snippet shows you an example of a very specific
authorization policy, which allows unauthenticated users to access to
the MQTT broker on the condition that they establish a dedicated
connection without management of session persistence:

</div>

<div class="listingblock">

<div class="content">

``` {.CodeRay .highlight}
@Override
public boolean canConnect(String sessionId, String clientId, String brokerAddress,
  MqttConnectOptions connectOptions) throws HookException {

  String mqttUser = connectOptions.getUsername();

  // If no credentials are provided, allow only NOT persistent sessions
  if (mqttUser == null) {
    boolean dedicatedConnection = !clientId.trim().isEmpty();
    boolean sessionPersistent = !connectOptions.isCleanSession();
    if (dedicatedConnection && sessionPersistent) {
      throw new HookException(201, "Cannot establish a connection with persistent session for NOT authenticated user");
    }
    return true;
  }

  // Otherwise, simply check the provided credentials
  String mqttPassword = connectOptions.getPassword();
  String storedPassword = lookupPasswordForMQTT(mqttUser);
  if (storedPassword == null) {
    throw new HookException(202, "User \"" + mqttUser + "\" not found");
  }

  return storedPassword.equals(mqttPassword);
}
```

</div>

</div>

<div class="paragraph">

Inspecting the `connectOptions` parameter helps you to easily accomplish
the task, as it contains the options being actually used by the
MQTT.Cool server to connect to the target MQTT broker. See the
[`MqttConnectOptions`](http://www.lightstreamer.com/api/mqtt.cool-hook-sdk/latest/cool/mqtt/hooks/MqttConnectOptions.html)
API reference for more detailed information.

</div>

<div class="paragraph">

On the client side, you will be notified about the raised authorization
issue by means of the related callback function, as described in
[Section 3.7, “Specifying Connection Options”](#connection_options):

</div>

<div class="listingblock">

<div class="content">

``` {.CodeRay .highlight}
connectOptions.onNotAuthorized = function(responseObject) {
  // responseObject is:
  //  - undefined in case of simple password mismatch
  //  - populated with errorCode and errorMessage according to
  //    the thrown HookException
  console.log('Connection NOT authorized');

  if (!responseObject) {
    console.log('Authentication failure');
    // Here the actions to be undertaken for handling authentication failure
  } else {
    switch(responseObject.errorCode) {
      case 201:
        // Here the actions to be undertaken for handling the authorization issue due
        // to unauthenticated user trying to connect with a persistent session
        ...
        break;

      case 202:
        // Here the actions to be undertaken for handling the authorization issue due
        // to not found user
        ...
        break;
    }
  }
};
```

</div>

</div>

<div class="paragraph">

Similarly to the `onConnectionFailure` callback, here the
`responseObject` parameter is passed only when a `HookException` has
been thrown on the server side, thus allowing you to differentiate the
kind of problem by looking at the `errorCode` and `errorMessage`
properties, which reflects respectively the code and the message as
embedded into the exception.

</div>

<div class="paragraph">

The following sequence diagram shows the interactions required to
establish an authorized end-to-end connection between the client and the
target MQTT broker.

</div>

<div class="imageblock" style="text-align: center">

<div class="content">

![can
connect](data:image/svg+xml;base64,PCFET0NUWVBFIHN2ZyBQVUJMSUMgIi0vL1czQy8vRFREIFNWRyAxLjEvL0VOIiAiaHR0cDovL3d3dy53My5vcmcvR3JhcGhpY3MvU1ZHLzEuMS9EVEQvc3ZnMTEuZHRkIj4KPHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHhtbG5zOnhsaW5rPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hsaW5rIiB3aWR0aD0iODY2cHgiIGhlaWdodD0iNjkxcHgiIHZlcnNpb249IjEuMSIgc3R5bGU9ImJhY2tncm91bmQtY29sb3I6IHJnYigyNTUsIDI1NSwgMjU1KTsiPjxkZWZzLz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgwLjUsMC41KSI+PHBhdGggZD0iTSA3NDIgMzMyIEwgNTA5LjI0IDMzMiIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHN0cm9rZS1kYXNoYXJyYXk9IjMgMyIgcG9pbnRlci1ldmVudHM9Im5vbmUiLz48cGF0aCBkPSJNIDUxNy4xMiAzMjcuNSBMIDUwOC4xMiAzMzIgTCA1MTcuMTIgMzM2LjUiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0ibm9uZSIvPjxnIGZpbGw9IiMwMDAwMDAiIGZvbnQtZmFtaWx5PSJIZWx2ZXRpY2EiIHRleHQtYW5jaG9yPSJtaWRkbGUiIGZvbnQtc2l6ZT0iMTFweCI+PHRleHQgeD0iNjIzLjUiIHk9IjMxNy41Ij5yZXR1cm4gVHJ1ZSBvciBGYWxzZSBvciB0aHJvdyBIb29rRXhjZXB0aW9uPC90ZXh0PjwvZz48cmVjdCB4PSIwIiB5PSIwIiB3aWR0aD0iODAiIGhlaWdodD0iNDAiIGZpbGw9IiNmZmYyY2MiIHN0cm9rZT0iIzAwMDAwMCIgcG9pbnRlci1ldmVudHM9Im5vbmUiLz48cGF0aCBkPSJNIDQwIDQwIEwgNDAgNjkwIiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgc3Ryb2tlLWRhc2hhcnJheT0iMyAzIiBwb2ludGVyLWV2ZW50cz0ibm9uZSIvPjxnIGZpbGw9IiMwMDAwMDAiIGZvbnQtZmFtaWx5PSJIZWx2ZXRpY2EiIGZvbnQtd2VpZ2h0PSJib2xkIiB0ZXh0LWFuY2hvcj0ibWlkZGxlIiBmb250LXNpemU9IjExcHgiPjx0ZXh0IHg9IjM5LjUiIHk9IjI0Ij46V2ViIENsaWVudDwvdGV4dD48L2c+PHJlY3QgeD0iMzUiIHk9IjkwIiB3aWR0aD0iMTAiIGhlaWdodD0iNTkiIGZpbGw9IiNmZmZmZmYiIHN0cm9rZT0iIzAwMDAwMCIgcG9pbnRlci1ldmVudHM9Im5vbmUiLz48cmVjdCB4PSIzNSIgeT0iMTkxIiB3aWR0aD0iMTAiIGhlaWdodD0iNTUiIGZpbGw9IiNmZmZmZmYiIHN0cm9rZT0iIzAwMDAwMCIgcG9pbnRlci1ldmVudHM9Im5vbmUiLz48cGF0aCBkPSJNIDE1NyAxMDggTCAyMTcuODggMTA4IiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9Im5vbmUiLz48cGF0aCBkPSJNIDIyNC44OCAxMDggTCAyMTcuODggMTExLjUgTCAyMTcuODggMTA0LjUgWiIgZmlsbD0iIzAwMDAwMCIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJub25lIi8+PGcgZmlsbD0iIzAwMDAwMCIgZm9udC1mYW1pbHk9IkhlbHZldGljYSIgdGV4dC1hbmNob3I9Im1pZGRsZSIgZm9udC1zaXplPSIxMXB4Ij48cmVjdCBmaWxsPSIjZmZmZmZmIiBzdHJva2U9Im5vbmUiIHg9IjE4MSIgeT0iOTMiIHdpZHRoPSIyMyIgaGVpZ2h0PSIxNCIgc3Ryb2tlLXdpZHRoPSIwIi8+PHRleHQgeD0iMTkxLjUiIHk9IjEwMS41Ij5uZXc8L3RleHQ+PC9nPjxyZWN0IHg9IjM1IiB5PSI0NjAiIHdpZHRoPSIxMCIgaGVpZ2h0PSI2MSIgZmlsbD0iI2ZmZmZmZiIgc3Ryb2tlPSIjMDAwMDAwIiBwb2ludGVyLWV2ZW50cz0ibm9uZSIvPjxwYXRoIGQ9Ik0gNDk3IDQzMCBMIDI3MS4yNCA0MzAiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBzdHJva2UtZGFzaGFycmF5PSIzIDMiIHBvaW50ZXItZXZlbnRzPSJub25lIi8+PHBhdGggZD0iTSAyNzkuMTIgNDI1LjUgTCAyNzAuMTIgNDMwIEwgMjc5LjEyIDQzNC41IiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9Im5vbmUiLz48ZyBmaWxsPSIjMDAwMDAwIiBmb250LWZhbWlseT0iSGVsdmV0aWNhIiBmb250LXN0eWxlPSJpdGFsaWMiIHRleHQtYW5jaG9yPSJtaWRkbGUiIGZvbnQtc2l6ZT0iMTFweCI+PHJlY3QgZmlsbD0iI2ZmZmZmZiIgc3Ryb2tlPSJub25lIiB4PSIzNTYiIHk9IjQxNSIgd2lkdGg9IjU1IiBoZWlnaHQ9IjE0IiBzdHJva2Utd2lkdGg9IjAiLz48dGV4dCB4PSIzODIuNSIgeT0iNDIzLjUiPmNvbm5lY3RlZDwvdGV4dD48L2c+PHJlY3QgeD0iNzEzIiB5PSIwIiB3aWR0aD0iNTkiIGhlaWdodD0iNDAiIGZpbGw9IiNmZmYyY2MiIHN0cm9rZT0iIzAwMDAwMCIgcG9pbnRlci1ldmVudHM9Im5vbmUiLz48cGF0aCBkPSJNIDc0Mi41IDQwIEwgNzQyLjUgNjkwIiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgc3Ryb2tlLWRhc2hhcnJheT0iMyAzIiBwb2ludGVyLWV2ZW50cz0ibm9uZSIvPjxnIGZpbGw9IiMwMDAwMDAiIGZvbnQtZmFtaWx5PSJIZWx2ZXRpY2EiIGZvbnQtd2VpZ2h0PSJib2xkIiB0ZXh0LWFuY2hvcj0ibWlkZGxlIiBmb250LXNpemU9IjExcHgiPjx0ZXh0IHg9Ijc0MiIgeT0iMjQiPjpIb29rPC90ZXh0PjwvZz48cmVjdCB4PSI3MzgiIHk9IjI5MiIgd2lkdGg9IjEwIiBoZWlnaHQ9IjQwIiBmaWxsPSIjZmZmZmZmIiBzdHJva2U9IiMwMDAwMDAiIHBvaW50ZXItZXZlbnRzPSJub25lIi8+PHJlY3QgeD0iMjI1IiB5PSIxMDAiIHdpZHRoPSI4MCIgaGVpZ2h0PSI0MCIgZmlsbD0iI2ZmZjJjYyIgc3Ryb2tlPSIjMDAwMDAwIiBwb2ludGVyLWV2ZW50cz0ibm9uZSIvPjxwYXRoIGQ9Ik0gMjY1IDE0MCBMIDI2NSA2ODgiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBzdHJva2UtZGFzaGFycmF5PSIzIDMiIHBvaW50ZXItZXZlbnRzPSJub25lIi8+PGcgZmlsbD0iIzAwMDAwMCIgZm9udC1mYW1pbHk9IkhlbHZldGljYSIgZm9udC13ZWlnaHQ9ImJvbGQiIHRleHQtYW5jaG9yPSJtaWRkbGUiIGZvbnQtc2l6ZT0iMTFweCI+PHRleHQgeD0iMjY0LjUiIHk9IjEyNCI+Ok1xdHRDbGllbnQ8L3RleHQ+PC9nPjxyZWN0IHg9IjI2MCIgeT0iMTg5IiB3aWR0aD0iMTAiIGhlaWdodD0iNTciIGZpbGw9IiNmZmZmZmYiIHN0cm9rZT0iIzAwMDAwMCIgcG9pbnRlci1ldmVudHM9Im5vbmUiLz48cmVjdCB4PSIzNiIgeT0iNjExIiB3aWR0aD0iMTAiIGhlaWdodD0iNTAiIGZpbGw9IiNmZmZmZmYiIHN0cm9rZT0iIzAwMDAwMCIgcG9pbnRlci1ldmVudHM9Im5vbmUiLz48cmVjdCB4PSIyNjAiIHk9IjU3MCIgd2lkdGg9IjEwIiBoZWlnaHQ9IjQwIiBmaWxsPSIjZmZmZmZmIiBzdHJva2U9IiMwMDAwMDAiIHBvaW50ZXItZXZlbnRzPSJub25lIi8+PHBhdGggZD0iTSAyNjQgNjEwIEwgNTQuMTIgNjEwLjk2IiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9Im5vbmUiLz48cGF0aCBkPSJNIDQ3LjEyIDYxMC45OSBMIDU0LjEgNjA3LjQ2IEwgNTQuMTMgNjE0LjQ2IFoiIGZpbGw9IiMwMDAwMDAiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0ibm9uZSIvPjxnIGZpbGw9IiMwMDAwMDAiIGZvbnQtZmFtaWx5PSJIZWx2ZXRpY2EiIHRleHQtYW5jaG9yPSJtaWRkbGUiIGZvbnQtc2l6ZT0iMTFweCI+PHJlY3QgZmlsbD0iI2ZmZmZmZiIgc3Ryb2tlPSJub25lIiB4PSIxMTIiIHk9IjU5NSIgd2lkdGg9Ijg3IiBoZWlnaHQ9IjE0IiBzdHJva2Utd2lkdGg9IjAiLz48dGV4dCB4PSIxNTQuNSIgeT0iNjA0Ij5vbk5vdEF1dGhvcml6ZWQ8L3RleHQ+PC9nPjxyZWN0IHg9Ijc4NSIgeT0iMCIgd2lkdGg9IjgwIiBoZWlnaHQ9IjQwIiBmaWxsPSIjZmZmMmNjIiBzdHJva2U9IiMwMDAwMDAiIHBvaW50ZXItZXZlbnRzPSJub25lIi8+PHBhdGggZD0iTSA4MjUgNDAgTCA4MjUgNjkwIiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgc3Ryb2tlLWRhc2hhcnJheT0iMyAzIiBwb2ludGVyLWV2ZW50cz0ibm9uZSIvPjxnIGZpbGw9IiMwMDAwMDAiIGZvbnQtZmFtaWx5PSJIZWx2ZXRpY2EiIGZvbnQtd2VpZ2h0PSJib2xkIiB0ZXh0LWFuY2hvcj0ibWlkZGxlIiBmb250LXNpemU9IjExcHgiPjx0ZXh0IHg9IjgyNC41IiB5PSIyNCI+Ok1RVFQgQnJva2VyPC90ZXh0PjwvZz48cmVjdCB4PSI4MjAiIHk9IjM4MCIgd2lkdGg9IjEwIiBoZWlnaHQ9IjMwIiBmaWxsPSIjZmZmZmZmIiBzdHJva2U9IiMwMDAwMDAiIHBvaW50ZXItZXZlbnRzPSJub25lIi8+PHBhdGggZD0iTSA1MDIuNSAzODAgTCA4MTEuODggMzgwIiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9Im5vbmUiLz48cGF0aCBkPSJNIDgxOC44OCAzODAgTCA4MTEuODggMzgzLjUgTCA4MTEuODggMzc2LjUgWiIgZmlsbD0iIzAwMDAwMCIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJub25lIi8+PGcgZmlsbD0iIzAwMDAwMCIgZm9udC1mYW1pbHk9IkhlbHZldGljYSIgZm9udC13ZWlnaHQ9ImJvbGQiIHRleHQtYW5jaG9yPSJtaWRkbGUiIGZvbnQtc2l6ZT0iMTFweCI+PHJlY3QgZmlsbD0iI2ZmZmZmZiIgc3Ryb2tlPSJub25lIiB4PSI2MzQiIHk9IjM2NSIgd2lkdGg9IjU2IiBoZWlnaHQ9IjE0IiBzdHJva2Utd2lkdGg9IjAiLz48dGV4dCB4PSI2NjEiIHk9IjM3My41Ij5DT05ORUNUPC90ZXh0PjwvZz48cGF0aCBkPSJNIDgyMSA0MTAgTCA1MDkuMjQgNDEwIiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgc3Ryb2tlLWRhc2hhcnJheT0iMyAzIiBwb2ludGVyLWV2ZW50cz0ibm9uZSIvPjxwYXRoIGQ9Ik0gNTE3LjEyIDQwNS41IEwgNTA4LjEyIDQxMCBMIDUxNy4xMiA0MTQuNSIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJub25lIi8+PGcgZmlsbD0iIzAwMDAwMCIgZm9udC1mYW1pbHk9IkhlbHZldGljYSIgZm9udC13ZWlnaHQ9ImJvbGQiIHRleHQtYW5jaG9yPSJtaWRkbGUiIGZvbnQtc2l6ZT0iMTFweCI+PHJlY3QgZmlsbD0iI2ZmZmZmZiIgc3Ryb2tlPSJub25lIiB4PSI2MzUiIHk9IjM5NSIgd2lkdGg9IjU5IiBoZWlnaHQ9IjE0IiBzdHJva2Utd2lkdGg9IjAiLz48dGV4dCB4PSI2NjMuNSIgeT0iNDAzLjUiPkNPTk5BQ0s8L3RleHQ+PC9nPjxyZWN0IHg9IjQ0MyIgeT0iMCIgd2lkdGg9IjEyMCIgaGVpZ2h0PSI0MCIgZmlsbD0iI2ZmZjJjYyIgc3Ryb2tlPSIjMDAwMDAwIiBwb2ludGVyLWV2ZW50cz0ibm9uZSIvPjxwYXRoIGQ9Ik0gNTAzIDQwIEwgNTAzIDY5MCIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHN0cm9rZS1kYXNoYXJyYXk9IjMgMyIgcG9pbnRlci1ldmVudHM9Im5vbmUiLz48ZyBmaWxsPSIjMDAwMDAwIiBmb250LWZhbWlseT0iSGVsdmV0aWNhIiBmb250LXdlaWdodD0iYm9sZCIgdGV4dC1hbmNob3I9Im1pZGRsZSIgZm9udC1zaXplPSIxMXB4Ij48dGV4dCB4PSI1MDIuNSIgeT0iMjQiPjpNUVRULkNvb2zCoFNlcnZlcjwvdGV4dD48L2c+PHJlY3QgeD0iNDk3IiB5PSIxOTUiIHdpZHRoPSIxMCIgaGVpZ2h0PSIzNzUiIGZpbGw9IiNmZmZmZmYiIHN0cm9rZT0iIzAwMDAwMCIgcG9pbnRlci1ldmVudHM9Im5vbmUiLz48cmVjdCB4PSI1MDMiIHk9IjIzNiIgd2lkdGg9IjEwIiBoZWlnaHQ9IjQwIiBmaWxsPSIjZmZmZmZmIiBzdHJva2U9IiMwMDAwMDAiIHBvaW50ZXItZXZlbnRzPSJub25lIi8+PHBhdGggZD0iTSA1MDggMjA3IEwgNTQwIDIwNyBMIDU0MCAyMzYgTCA1MjEuMTIgMjM2IiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9Im5vbmUiLz48cGF0aCBkPSJNIDUxNC4xMiAyMzYgTCA1MjEuMTIgMjMyLjUgTCA1MjEuMTIgMjM5LjUgWiIgZmlsbD0iIzAwMDAwMCIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJub25lIi8+PGcgZmlsbD0iIzAwMDAwMCIgZm9udC1mYW1pbHk9IkhlbHZldGljYSIgZm9udC1zdHlsZT0iaXRhbGljIiBmb250LXNpemU9IjExcHgiPjxyZWN0IGZpbGw9IiNmZmZmZmYiIHN0cm9rZT0ibm9uZSIgeD0iNTQ0IiB5PSIyMTMiIHdpZHRoPSIxMzUiIGhlaWdodD0iMTQiIHN0cm9rZS13aWR0aD0iMCIvPjx0ZXh0IHg9IjU0My41IiB5PSIyMjIiPmxvb2t1cENvbmZpZ3VyYXRpb24oYWxpYXMpPC90ZXh0PjwvZz48cmVjdCB4PSIxMDAiIHk9IjAiIHdpZHRoPSIxMTMiIGhlaWdodD0iNDAiIGZpbGw9IiNmZmYyY2MiIHN0cm9rZT0iIzAwMDAwMCIgcG9pbnRlci1ldmVudHM9Im5vbmUiLz48cGF0aCBkPSJNIDE1Ni41IDQwIEwgMTU2LjUgNjkwIiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgc3Ryb2tlLWRhc2hhcnJheT0iMyAzIiBwb2ludGVyLWV2ZW50cz0ibm9uZSIvPjxnIGZpbGw9IiMwMDAwMDAiIGZvbnQtZmFtaWx5PSJIZWx2ZXRpY2EiIGZvbnQtd2VpZ2h0PSJib2xkIiB0ZXh0LWFuY2hvcj0ibWlkZGxlIiBmb250LXNpemU9IjExcHgiPjx0ZXh0IHg9IjE1NiIgeT0iMjQiPjpNUVRUQ29vbFNlc3Npb248L3RleHQ+PC9nPjxyZWN0IHg9IjE1MiIgeT0iMTAwIiB3aWR0aD0iMTAiIGhlaWdodD0iNTAiIGZpbGw9IiNmZmZmZmYiIHN0cm9rZT0iIzAwMDAwMCIgcG9pbnRlci1ldmVudHM9Im5vbmUiLz48cGF0aCBkPSJNIDQ1IDEwMCBMIDE0My44OCAxMDAiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0ibm9uZSIvPjxwYXRoIGQ9Ik0gMTUwLjg4IDEwMCBMIDE0My44OCAxMDMuNSBMIDE0My44OCA5Ni41IFoiIGZpbGw9IiMwMDAwMDAiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0ibm9uZSIvPjxnIGZpbGw9IiMwMDAwMDAiIGZvbnQtZmFtaWx5PSJIZWx2ZXRpY2EiIHRleHQtYW5jaG9yPSJtaWRkbGUiIGZvbnQtc2l6ZT0iMTFweCI+PHRleHQgeD0iOTguNSIgeT0iOTMuNSI+Y3JlYXRlQ2xpZW50KGFsaWFzKTwvdGV4dD48L2c+PHBhdGggZD0iTSAxNTIgMTQ5IEwgNDcuMjQgMTQ5IiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgc3Ryb2tlLWRhc2hhcnJheT0iMyAzIiBwb2ludGVyLWV2ZW50cz0ibm9uZSIvPjxwYXRoIGQ9Ik0gNTUuMTIgMTQ0LjUgTCA0Ni4xMiAxNDkgTCA1NS4xMiAxNTMuNSIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJub25lIi8+PHBhdGggZD0iTSA0MyAxOTEgTCAyNTEuODggMTg5LjA3IiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9Im5vbmUiLz48cGF0aCBkPSJNIDI1OC44OCAxODkuMDEgTCAyNTEuOTEgMTkyLjU3IEwgMjUxLjg1IDE4NS41NyBaIiBmaWxsPSIjMDAwMDAwIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9Im5vbmUiLz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSg5Mi41LDE3NS41KSI+PHN3aXRjaD48Zm9yZWlnbk9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6dmlzaWJsZTsiIHBvaW50ZXItZXZlbnRzPSJhbGwiIHdpZHRoPSIxMTgiIGhlaWdodD0iMTEiIHJlcXVpcmVkRmVhdHVyZXM9Imh0dHA6Ly93d3cudzMub3JnL1RSL1NWRzExL2ZlYXR1cmUjRXh0ZW5zaWJpbGl0eSI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6IGlubGluZS1ibG9jazsgZm9udC1zaXplOiAxMXB4OyBmb250LWZhbWlseTogSGVsdmV0aWNhOyBjb2xvcjogcmdiKDAsIDAsIDApOyBsaW5lLWhlaWdodDogMS4yOyB2ZXJ0aWNhbC1hbGlnbjogdG9wOyB3aGl0ZS1zcGFjZTogbm93cmFwOyB0ZXh0LWFsaWduOiBjZW50ZXI7Ij48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTppbmxpbmUtYmxvY2s7dGV4dC1hbGlnbjppbmhlcml0O3RleHQtZGVjb3JhdGlvbjppbmhlcml0O2JhY2tncm91bmQtY29sb3I6I2ZmZmZmZjsiPmNvbm5lY3QoY2xpZW50X29wdGlvbnMpPC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0Pjx0ZXh0IHg9IjU5IiB5PSIxMSIgZmlsbD0iIzAwMDAwMCIgdGV4dC1hbmNob3I9Im1pZGRsZSIgZm9udC1zaXplPSIxMXB4IiBmb250LWZhbWlseT0iSGVsdmV0aWNhIj5jb25uZWN0KGNsaWVudF9vcHRpb25zKTwvdGV4dD48L3N3aXRjaD48L2c+PHBhdGggZD0iTSAyNzAgMTk1IEwgNDg4Ljg4IDE5NSIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJub25lIi8+PHBhdGggZD0iTSA0OTUuODggMTk1IEwgNDg4Ljg4IDE5OC41IEwgNDg4Ljg4IDE5MS41IFoiIGZpbGw9IiMwMDAwMDAiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0ibm9uZSIvPjxnIGZpbGw9IiMwMDAwMDAiIGZvbnQtZmFtaWx5PSJIZWx2ZXRpY2EiIGZvbnQtc3R5bGU9Iml0YWxpYyIgdGV4dC1hbmNob3I9Im1pZGRsZSIgZm9udC1zaXplPSIxMXB4Ij48dGV4dCB4PSIzODMuNSIgeT0iMTg4LjUiPmNvbm5lY3RfdG9fYnJva2VyKGFsaWFzLCBjbGllbnRfb3B0aW9ucyk8L3RleHQ+PC9nPjxwYXRoIGQ9Ik0gNTA3IDI5MiBMIDcyOS44OCAyOTIiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0ibm9uZSIvPjxwYXRoIGQ9Ik0gNzM2Ljg4IDI5MiBMIDcyOS44OCAyOTUuNSBMIDcyOS44OCAyODguNSBaIiBmaWxsPSIjMDAwMDAwIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9Im5vbmUiLz48ZyBmaWxsPSIjMDAwMDAwIiBmb250LWZhbWlseT0iSGVsdmV0aWNhIiB0ZXh0LWFuY2hvcj0ibWlkZGxlIiBmb250LXNpemU9IjExcHgiPjx0ZXh0IHg9IjYyMi41IiB5PSIyODUuNSI+Y2FuQ29ubmVjdChicm9rZXJBZGRyZXNzLCBvcHRpb25zKTwvdGV4dD48L2c+PHJlY3QgeD0iMjYwIiB5PSI0MzAiIHdpZHRoPSIxMCIgaGVpZ2h0PSIzMCIgZmlsbD0iI2ZmZmZmZiIgc3Ryb2tlPSIjMDAwMDAwIiBwb2ludGVyLWV2ZW50cz0ibm9uZSIvPjxwYXRoIGQ9Ik0gMjYzIDI0NSBMIDQ2LjI0IDI0NS45OSIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHN0cm9rZS1kYXNoYXJyYXk9IjMgMyIgcG9pbnRlci1ldmVudHM9Im5vbmUiLz48cGF0aCBkPSJNIDU0LjEgMjQxLjQ1IEwgNDUuMTIgMjQ1Ljk5IEwgNTQuMTQgMjUwLjQ1IiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9Im5vbmUiLz48cGF0aCBkPSJNIDIwIDM1MCBMIDgwIDM1MCBMIDgwIDM2NSBMIDcwIDM4MCBMIDIwIDM4MCBaIiBmaWxsPSIjMzNmZmZmIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS13aWR0aD0iMiIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0ibm9uZSIvPjxwYXRoIGQ9Ik0gODAgMzUwIEwgODUwIDM1MCBMIDg1MCA2ODAgTCAyMCA2ODAgTCAyMCAzODAiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLXdpZHRoPSIyIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJub25lIi8+PGcgZmlsbD0iIzAwMDAwMCIgZm9udC1mYW1pbHk9IkhlbHZldGljYSIgdGV4dC1hbmNob3I9Im1pZGRsZSIgZm9udC1zaXplPSIxMXB4Ij48dGV4dCB4PSI1MC41IiB5PSIzNjkiPmFsdDwvdGV4dD48L2c+PHBhdGggZD0iTSA0OTcgNTcwIEwgMjcyLjI0IDU3MC45OSIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHN0cm9rZS1kYXNoYXJyYXk9IjMgMyIgcG9pbnRlci1ldmVudHM9Im5vbmUiLz48cGF0aCBkPSJNIDI4MC4xIDU2Ni40NiBMIDI3MS4xMiA1NzEgTCAyODAuMTQgNTc1LjQ2IiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9Im5vbmUiLz48ZyBmaWxsPSIjMDAwMDAwIiBmb250LWZhbWlseT0iSGVsdmV0aWNhIiBmb250LXN0eWxlPSJpdGFsaWMiIHRleHQtYW5jaG9yPSJtaWRkbGUiIGZvbnQtc2l6ZT0iMTFweCI+PHJlY3QgZmlsbD0iI2ZmZmZmZiIgc3Ryb2tlPSJub25lIiB4PSIzMzQiIHk9IjU1NSIgd2lkdGg9IjEwMCIgaGVpZ2h0PSIxNCIgc3Ryb2tlLXdpZHRoPSIwIi8+PHRleHQgeD0iMzgyLjUiIHk9IjU2NCI+YXV0aG9yaXphdGlvbl9pc3N1ZTwvdGV4dD48L2c+PHBhdGggZD0iTSAyMSA1NDQgTCA4NTAgNTQ0IiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS13aWR0aD0iMiIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBzdHJva2UtZGFzaGFycmF5PSI2IDYiIHBvaW50ZXItZXZlbnRzPSJub25lIi8+PGcgZmlsbD0iIzAwMDAwMCIgZm9udC1mYW1pbHk9IkhlbHZldGljYSIgZm9udC13ZWlnaHQ9ImJvbGQiIGZvbnQtc2l6ZT0iMTFweCI+PHRleHQgeD0iNDcuNSIgeT0iNDAzIj5bSG9vayByZXR1cm5zIFRydWVdPC90ZXh0PjwvZz48ZyBmaWxsPSIjMDAwMDAwIiBmb250LWZhbWlseT0iSGVsdmV0aWNhIiBmb250LXdlaWdodD0iYm9sZCIgZm9udC1zaXplPSIxMXB4Ij48dGV4dCB4PSI0Ny41IiB5PSI1NjcuNSI+W0hvb2sgcmV0dXJucyBGYWxzZTwvdGV4dD48dGV4dCB4PSI0Ny41IiB5PSI1ODAuNSI+b3IgdGhyb3cgSG9va0V4Y2VwdGlvbl08L3RleHQ+PC9nPjxwYXRoIGQ9Ik0gMjY0IDQ2MCBMIDUzLjEyIDQ2MCIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJub25lIi8+PHBhdGggZD0iTSA0Ni4xMiA0NjAgTCA1My4xMiA0NTYuNSBMIDUzLjEyIDQ2My41IFoiIGZpbGw9IiMwMDAwMDAiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0ibm9uZSIvPjxnIGZpbGw9IiMwMDAwMDAiIGZvbnQtZmFtaWx5PSJIZWx2ZXRpY2EiIHRleHQtYW5jaG9yPSJtaWRkbGUiIGZvbnQtc2l6ZT0iMTFweCI+PHJlY3QgZmlsbD0iI2ZmZmZmZiIgc3Ryb2tlPSJub25lIiB4PSI5NyIgeT0iNDQ1IiB3aWR0aD0iMTE1IiBoZWlnaHQ9IjE0IiBzdHJva2Utd2lkdGg9IjAiLz48dGV4dCB4PSIxNTMuNSIgeT0iNDUzLjUiPm9uQ29ubmVjdGlvblN1Y2Nlc3M8L3RleHQ+PC9nPjwvZz48L3N2Zz4=)

</div>

<div class="title">

Figure 12. Sequence diagram for connection creation

</div>

</div>

<div class="sect4">

##### Providing Broker Configuration {#hook_broker_configuration}

<div class="paragraph">

As already anticipated in [Section 2.1.1, “The Hook
Variant”](#static_lookup_hook), you can program your custom Hook to
provide a valid MQTT broker configuration for a specific connection
alias, when no other static entries have been supplied in the
`mqtt_master_connector_conf.xml` file for the same alias. All you need
is to override the `resolveAlias` method, where you will provide an
instance of the
[`MqttBrokerConfig`](http://www.lightstreamer.com/api/mqtt.cool-hook-sdk/latest/cool/mqtt/hooks/MqttBrokerConfig.html)
interface, which will act as an MQTT broker configuration as it was
provided from the static configuration:

</div>

<div class="listingblock">

<div class="content">

``` {.CodeRay .highlight}
import cool.mqtt.hooks.utils.MqttBrokerConfigBuilder;

...

@Override
public MqttBrokerConfig resolveAlias(String alias) throws HookException {
  /*
   * If a client wants to connect to the MQTT broker aliased
   * by "my_cool_broker", provide a valid configuration.
   */
   if ("my_cool_broker".equals(alias)) {
     MqttBrokerConfig config =
       new MqttBrokerConfigBuilder("tcp://my.cool.broker:1883")
         .connectionTimeout(10)
         .keepAlive(20)
         .clientIdPrefix("COOL_BROKER")
         .build();
     return config;
   }

   return null;
}
```

</div>

</div>

<div class="paragraph">

As shown above, you can also take benefit of the
[`MqttBrokerConfigBuilder`](http://www.lightstreamer.com/api/mqtt.cool-hook-sdk/latest/cool/mqtt/hooks/utils/MqttBrokerConfigBuilder.html)
utility class, which is a *builder* designed to simplify the making of
an `MqttBrokerConfig` instance.

</div>

<div class="admonitionblock note">

  ---- ---------------------------------------------------------------------------------------------------------------------------------------------------
  **   Through `MqttBrokerConfig` you can set all the same configuration parameters already discussed in [Section 2.1, “Static Lookup”](#static_lookup).
  ---- ---------------------------------------------------------------------------------------------------------------------------------------------------

</div>

<div class="paragraph">

On the other hand, if no configuration is available for the provided
connection alias (neither from `mqtt_master_connector_conf.xml` nor from
the Hook), on the client side the
[`onFailure`](http://www.lightstreamer.com/api/mqtt.cool-web-client/latest/global.html#onConnectionFailure)
callback function is invoked, with the relative
`responseObject.errorCode` value:

</div>

<div class="listingblock">

<div class="content">

``` {.CodeRay .highlight}
...
var mqttClient = mqttCoolSession.createClient('not_existing_connection_alias');

mqttClient.connect({

  onFailure: function(responseObject) {
    switch(responseObject.errorCode) {
      ...

      case 9:
        console.log('No valid configuration found');
        ...
      break
      ...
    }
  }

});
...
```

</div>

</div>

<div class="paragraph">

The following diagram illustrates how the Hook is involved in providing
a valid configuration.

</div>

<div class="imageblock" style="text-align: center">

<div class="content">

![resolve
alias](data:image/svg+xml;base64,PCFET0NUWVBFIHN2ZyBQVUJMSUMgIi0vL1czQy8vRFREIFNWRyAxLjEvL0VOIiAiaHR0cDovL3d3dy53My5vcmcvR3JhcGhpY3MvU1ZHLzEuMS9EVEQvc3ZnMTEuZHRkIj4KPHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHhtbG5zOnhsaW5rPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hsaW5rIiB3aWR0aD0iODUycHgiIGhlaWdodD0iNjUxcHgiIHZlcnNpb249IjEuMSIgc3R5bGU9ImJhY2tncm91bmQtY29sb3I6IHJnYigyNTUsIDI1NSwgMjU1KTsiPjxkZWZzLz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgwLjUsMC41KSI+PHJlY3QgeD0iMCIgeT0iMCIgd2lkdGg9IjgwIiBoZWlnaHQ9IjQwIiBmaWxsPSIjZmZmMmNjIiBzdHJva2U9IiMwMDAwMDAiIHBvaW50ZXItZXZlbnRzPSJub25lIi8+PHBhdGggZD0iTSA0MCA0MCBMIDQwIDY1MCIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHN0cm9rZS1kYXNoYXJyYXk9IjMgMyIgcG9pbnRlci1ldmVudHM9Im5vbmUiLz48ZyBmaWxsPSIjMDAwMDAwIiBmb250LWZhbWlseT0iSGVsdmV0aWNhIiBmb250LXdlaWdodD0iYm9sZCIgdGV4dC1hbmNob3I9Im1pZGRsZSIgZm9udC1zaXplPSIxMXB4Ij48dGV4dCB4PSIzOS41IiB5PSIyNCI+OldlYiBDbGllbnQ8L3RleHQ+PC9nPjxyZWN0IHg9IjM1IiB5PSI5MCIgd2lkdGg9IjEwIiBoZWlnaHQ9IjU5IiBmaWxsPSIjMDAwMDAwIiBzdHJva2U9IiMwMDAwMDAiIHRyYW5zZm9ybT0idHJhbnNsYXRlKDIsMykiIG9wYWNpdHk9IjAuMjUiLz48cmVjdCB4PSIzNSIgeT0iOTAiIHdpZHRoPSIxMCIgaGVpZ2h0PSI1OSIgZmlsbD0iI2ZmZmZmZiIgc3Ryb2tlPSIjMDAwMDAwIiBwb2ludGVyLWV2ZW50cz0ibm9uZSIvPjxyZWN0IHg9IjM1IiB5PSIxOTQiIHdpZHRoPSIxMCIgaGVpZ2h0PSI1NiIgZmlsbD0iI2ZmZmZmZiIgc3Ryb2tlPSIjMDAwMDAwIiBwb2ludGVyLWV2ZW50cz0ibm9uZSIvPjxwYXRoIGQ9Ik0gMTY4IDExMSBMIDIxNy44OCAxMTEiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0ibm9uZSIvPjxwYXRoIGQ9Ik0gMjI0Ljg4IDExMSBMIDIxNy44OCAxMTQuNSBMIDIxNy44OCAxMDcuNSBaIiBmaWxsPSIjMDAwMDAwIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9Im5vbmUiLz48ZyBmaWxsPSIjMDAwMDAwIiBmb250LWZhbWlseT0iSGVsdmV0aWNhIiB0ZXh0LWFuY2hvcj0ibWlkZGxlIiBmb250LXNpemU9IjExcHgiPjxyZWN0IGZpbGw9IiNmZmZmZmYiIHN0cm9rZT0ibm9uZSIgeD0iMTg2IiB5PSI5NiIgd2lkdGg9IjIzIiBoZWlnaHQ9IjE0IiBzdHJva2Utd2lkdGg9IjAiLz48dGV4dCB4PSIxOTYuNSIgeT0iMTA0LjUiPm5ldzwvdGV4dD48L2c+PHJlY3QgeD0iNjkzIiB5PSIwIiB3aWR0aD0iNTkiIGhlaWdodD0iNDAiIGZpbGw9IiNmZmYyY2MiIHN0cm9rZT0iIzAwMDAwMCIgcG9pbnRlci1ldmVudHM9Im5vbmUiLz48cGF0aCBkPSJNIDcyMi41IDQwIEwgNzIyLjUgNjUwIiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgc3Ryb2tlLWRhc2hhcnJheT0iMyAzIiBwb2ludGVyLWV2ZW50cz0ibm9uZSIvPjxnIGZpbGw9IiMwMDAwMDAiIGZvbnQtZmFtaWx5PSJIZWx2ZXRpY2EiIGZvbnQtd2VpZ2h0PSJib2xkIiB0ZXh0LWFuY2hvcj0ibWlkZGxlIiBmb250LXNpemU9IjExcHgiPjx0ZXh0IHg9IjcyMiIgeT0iMjQiPjpIb29rPC90ZXh0PjwvZz48cmVjdCB4PSI3MTgiIHk9IjI5MiIgd2lkdGg9IjEwIiBoZWlnaHQ9IjQwIiBmaWxsPSIjZmZmZmZmIiBzdHJva2U9IiMwMDAwMDAiIHBvaW50ZXItZXZlbnRzPSJub25lIi8+PHJlY3QgeD0iMjI1IiB5PSIxMDQiIHdpZHRoPSI4MCIgaGVpZ2h0PSI0MCIgZmlsbD0iI2ZmZjJjYyIgc3Ryb2tlPSIjMDAwMDAwIiBwb2ludGVyLWV2ZW50cz0ibm9uZSIvPjxwYXRoIGQ9Ik0gMjY1IDE0NCBMIDI2NSA2NTAiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBzdHJva2UtZGFzaGFycmF5PSIzIDMiIHBvaW50ZXItZXZlbnRzPSJub25lIi8+PGcgZmlsbD0iIzAwMDAwMCIgZm9udC1mYW1pbHk9IkhlbHZldGljYSIgZm9udC13ZWlnaHQ9ImJvbGQiIHRleHQtYW5jaG9yPSJtaWRkbGUiIGZvbnQtc2l6ZT0iMTFweCI+PHRleHQgeD0iMjY0LjUiIHk9IjEyOCI+Ok1xdHRDbGllbnQ8L3RleHQ+PC9nPjxyZWN0IHg9IjI2MCIgeT0iMTkzIiB3aWR0aD0iMTAiIGhlaWdodD0iNTciIGZpbGw9IiNmZmZmZmYiIHN0cm9rZT0iIzAwMDAwMCIgcG9pbnRlci1ldmVudHM9Im5vbmUiLz48cmVjdCB4PSI3NzEiIHk9IjAiIHdpZHRoPSI4MCIgaGVpZ2h0PSI0MCIgZmlsbD0iI2ZmZjJjYyIgc3Ryb2tlPSIjMDAwMDAwIiBwb2ludGVyLWV2ZW50cz0ibm9uZSIvPjxwYXRoIGQ9Ik0gODExIDQwIEwgODExIDY1MCIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHN0cm9rZS1kYXNoYXJyYXk9IjMgMyIgcG9pbnRlci1ldmVudHM9Im5vbmUiLz48ZyBmaWxsPSIjMDAwMDAwIiBmb250LWZhbWlseT0iSGVsdmV0aWNhIiBmb250LXdlaWdodD0iYm9sZCIgdGV4dC1hbmNob3I9Im1pZGRsZSIgZm9udC1zaXplPSIxMXB4Ij48dGV4dCB4PSI4MTAuNSIgeT0iMjQiPjpNUVRUIEJyb2tlcjwvdGV4dD48L2c+PHJlY3QgeD0iNDM3IiB5PSIwIiB3aWR0aD0iMTMzIiBoZWlnaHQ9IjQwIiBmaWxsPSIjZmZmMmNjIiBzdHJva2U9IiMwMDAwMDAiIHBvaW50ZXItZXZlbnRzPSJub25lIi8+PHBhdGggZD0iTSA1MDMuNSA0MCBMIDUwMy41IDY1MCIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHN0cm9rZS1kYXNoYXJyYXk9IjMgMyIgcG9pbnRlci1ldmVudHM9Im5vbmUiLz48ZyBmaWxsPSIjMDAwMDAwIiBmb250LWZhbWlseT0iSGVsdmV0aWNhIiBmb250LXdlaWdodD0iYm9sZCIgdGV4dC1hbmNob3I9Im1pZGRsZSIgZm9udC1zaXplPSIxMXB4Ij48dGV4dCB4PSI1MDMiIHk9IjI0Ij46TVFUVC5Db29sIFNlcnZlcjwvdGV4dD48L2c+PHJlY3QgeD0iNDk5IiB5PSIyMDAiIHdpZHRoPSIxMCIgaGVpZ2h0PSIzMjAiIGZpbGw9IiNmZmZmZmYiIHN0cm9rZT0iIzAwMDAwMCIgcG9pbnRlci1ldmVudHM9Im5vbmUiLz48cmVjdCB4PSI1MDQiIHk9IjIzNiIgd2lkdGg9IjEwIiBoZWlnaHQ9IjQwIiBmaWxsPSIjZmZmZmZmIiBzdHJva2U9IiMwMDAwMDAiIHBvaW50ZXItZXZlbnRzPSJub25lIi8+PHBhdGggZD0iTSA1MDkgMjA3IEwgNTM0IDIwNyBMIDUzNCAyMzYgTCA1MjIuMTIgMjM2IiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9Im5vbmUiLz48cGF0aCBkPSJNIDUxNS4xMiAyMzYgTCA1MjIuMTIgMjMyLjUgTCA1MjIuMTIgMjM5LjUgWiIgZmlsbD0iIzAwMDAwMCIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJub25lIi8+PGcgZmlsbD0iIzAwMDAwMCIgZm9udC1mYW1pbHk9IkhlbHZldGljYSIgZm9udC1zdHlsZT0iaXRhbGljIiBmb250LXNpemU9IjExcHgiPjxyZWN0IGZpbGw9IiNmZmZmZmYiIHN0cm9rZT0ibm9uZSIgeD0iNTM4IiB5PSIyMTMiIHdpZHRoPSIxMzUiIGhlaWdodD0iMTQiIHN0cm9rZS13aWR0aD0iMCIvPjx0ZXh0IHg9IjUzNy41IiB5PSIyMjIiPmxvb2t1cENvbmZpZ3VyYXRpb24oYWxpYXMpPC90ZXh0PjwvZz48cmVjdCB4PSIxMDYiIHk9IjAiIHdpZHRoPSIxMTMiIGhlaWdodD0iNDAiIGZpbGw9IiNmZmYyY2MiIHN0cm9rZT0iIzAwMDAwMCIgcG9pbnRlci1ldmVudHM9Im5vbmUiLz48cGF0aCBkPSJNIDE2Mi41IDQwIEwgMTYyLjUgNjUwIiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgc3Ryb2tlLWRhc2hhcnJheT0iMyAzIiBwb2ludGVyLWV2ZW50cz0ibm9uZSIvPjxnIGZpbGw9IiMwMDAwMDAiIGZvbnQtZmFtaWx5PSJIZWx2ZXRpY2EiIGZvbnQtd2VpZ2h0PSJib2xkIiB0ZXh0LWFuY2hvcj0ibWlkZGxlIiBmb250LXNpemU9IjExcHgiPjx0ZXh0IHg9IjE2MiIgeT0iMjQiPjpNUVRUQ29vbFNlc3Npb248L3RleHQ+PC9nPjxyZWN0IHg9IjE1OCIgeT0iMTAwIiB3aWR0aD0iMTAiIGhlaWdodD0iNTAiIGZpbGw9IiMwMDAwMDAiIHN0cm9rZT0iIzAwMDAwMCIgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoMiwzKSIgb3BhY2l0eT0iMC4yNSIvPjxyZWN0IHg9IjE1OCIgeT0iMTAwIiB3aWR0aD0iMTAiIGhlaWdodD0iNTAiIGZpbGw9IiNmZmZmZmYiIHN0cm9rZT0iIzAwMDAwMCIgcG9pbnRlci1ldmVudHM9Im5vbmUiLz48cGF0aCBkPSJNIDQ1IDEwMCBMIDE0OS44OCAxMDAiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0ibm9uZSIvPjxwYXRoIGQ9Ik0gMTU2Ljg4IDEwMCBMIDE0OS44OCAxMDMuNSBMIDE0OS44OCA5Ni41IFoiIGZpbGw9IiMwMDAwMDAiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0ibm9uZSIvPjxnIGZpbGw9IiMwMDAwMDAiIGZvbnQtZmFtaWx5PSJIZWx2ZXRpY2EiIHRleHQtYW5jaG9yPSJtaWRkbGUiIGZvbnQtc2l6ZT0iMTFweCI+PHJlY3QgZmlsbD0iI2ZmZmZmZiIgc3Ryb2tlPSJub25lIiB4PSI1NiIgeT0iODUiIHdpZHRoPSI5NCIgaGVpZ2h0PSIxNCIgc3Ryb2tlLXdpZHRoPSIwIi8+PHRleHQgeD0iMTAxLjUiIHk9IjkzLjUiPmNyZWF0ZUNsaWVudChhbGlhcyk8L3RleHQ+PC9nPjxwYXRoIGQ9Ik0gMTU4IDE0OSBMIDQyLjI0IDE0OSIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHN0cm9rZS1kYXNoYXJyYXk9IjMgMyIgcG9pbnRlci1ldmVudHM9Im5vbmUiLz48cGF0aCBkPSJNIDUwLjEyIDE0NC41IEwgNDEuMTIgMTQ5IEwgNTAuMTIgMTUzLjUiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0ibm9uZSIvPjxwYXRoIGQ9Ik0gNDMgMTk0IEwgMjU1Ljg4IDE5My4wNCIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJub25lIi8+PHBhdGggZD0iTSAyNjIuODggMTkzLjAxIEwgMjU1LjkgMTk2LjU0IEwgMjU1Ljg3IDE4OS41NCBaIiBmaWxsPSIjMDAwMDAwIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9Im5vbmUiLz48ZyBmaWxsPSIjMDAwMDAwIiBmb250LWZhbWlseT0iSGVsdmV0aWNhIiB0ZXh0LWFuY2hvcj0ibWlkZGxlIiBmb250LXNpemU9IjExcHgiPjxyZWN0IGZpbGw9IiNmZmZmZmYiIHN0cm9rZT0ibm9uZSIgeD0iOTQiIHk9IjE3OCIgd2lkdGg9IjEyMCIgaGVpZ2h0PSIxNCIgc3Ryb2tlLXdpZHRoPSIwIi8+PHRleHQgeD0iMTUzLjUiIHk9IjE4NyI+Y29ubmVjdChjbGllbnRfb3B0aW9ucyk8L3RleHQ+PC9nPjxwYXRoIGQ9Ik0gMjcwIDIwMCBMIDQ5NS44OCAyMDAiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0ibm9uZSIvPjxwYXRoIGQ9Ik0gNTAyLjg4IDIwMCBMIDQ5NS44OCAyMDMuNSBMIDQ5NS44OCAxOTYuNSBaIiBmaWxsPSIjMDAwMDAwIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9Im5vbmUiLz48ZyBmaWxsPSIjMDAwMDAwIiBmb250LWZhbWlseT0iSGVsdmV0aWNhIiBmb250LXN0eWxlPSJpdGFsaWMiIHRleHQtYW5jaG9yPSJtaWRkbGUiIGZvbnQtc2l6ZT0iMTFweCI+PHJlY3QgZmlsbD0iI2ZmZmZmZiIgc3Ryb2tlPSJub25lIiB4PSIyODYiIHk9IjE4NSIgd2lkdGg9IjIwNCIgaGVpZ2h0PSIxNCIgc3Ryb2tlLXdpZHRoPSIwIi8+PHRleHQgeD0iMzg2LjUiIHk9IjE5My41Ij5jb25uZWN0X3RvX2Jyb2tlcihhbGlhcywgY2xpZW50X29wdGlvbnMpPC90ZXh0PjwvZz48cGF0aCBkPSJNIDUwOSAyOTIgTCA3MDkuODggMjkyIiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9Im5vbmUiLz48cGF0aCBkPSJNIDcxNi44OCAyOTIgTCA3MDkuODggMjk1LjUgTCA3MDkuODggMjg4LjUgWiIgZmlsbD0iIzAwMDAwMCIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJub25lIi8+PGcgZmlsbD0iIzAwMDAwMCIgZm9udC1mYW1pbHk9IkhlbHZldGljYSIgdGV4dC1hbmNob3I9Im1pZGRsZSIgZm9udC1zaXplPSIxMXB4Ij48cmVjdCBmaWxsPSIjZmZmZmZmIiBzdHJva2U9Im5vbmUiIHg9IjU2OCIgeT0iMjc3IiB3aWR0aD0iOTQiIGhlaWdodD0iMTQiIHN0cm9rZS13aWR0aD0iMCIvPjx0ZXh0IHg9IjYxMy41IiB5PSIyODUuNSI+cmVzb2x2ZUFsaWFzKGFsaWFzKTwvdGV4dD48L2c+PHBhdGggZD0iTSA3MjIgMzMyIEwgNTExLjI0IDMzMiIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHN0cm9rZS1kYXNoYXJyYXk9IjMgMyIgcG9pbnRlci1ldmVudHM9Im5vbmUiLz48cGF0aCBkPSJNIDUxOS4xMiAzMjcuNSBMIDUxMC4xMiAzMzIgTCA1MTkuMTIgMzM2LjUiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0ibm9uZSIvPjxnIGZpbGw9IiMwMDAwMDAiIGZvbnQtZmFtaWx5PSJIZWx2ZXRpY2EiIHRleHQtYW5jaG9yPSJtaWRkbGUiIGZvbnQtc2l6ZT0iMTFweCI+PHJlY3QgZmlsbD0iI2ZmZmZmZiIgc3Ryb2tlPSJub25lIiB4PSI1MjgiIHk9IjMxNyIgd2lkdGg9IjE3NSIgaGVpZ2h0PSIxNCIgc3Ryb2tlLXdpZHRoPSIwIi8+PHRleHQgeD0iNjE0LjUiIHk9IjMyNS41Ij5yZXR1cm4gQnJva2VyIENvbmZpZ3VyYXRpb24gb3IgbnVsbDwvdGV4dD48L2c+PHBhdGggZD0iTSAyNjMgMjQ5IEwgNDIuMjQgMjQ5Ljk5IiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgc3Ryb2tlLWRhc2hhcnJheT0iMyAzIiBwb2ludGVyLWV2ZW50cz0ibm9uZSIvPjxwYXRoIGQ9Ik0gNTAuMSAyNDUuNDUgTCA0MS4xMiAyNDkuOTkgTCA1MC4xNCAyNTQuNDUiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0ibm9uZSIvPjxyZWN0IHg9IjcxOCIgeT0iMzc0IiB3aWR0aD0iMTAiIGhlaWdodD0iNDAiIGZpbGw9IiNmZmZmZmYiIHN0cm9rZT0iIzAwMDAwMCIgcG9pbnRlci1ldmVudHM9Im5vbmUiLz48cGF0aCBkPSJNIDUwOSAzNzQgTCA3MDkuODggMzc0IiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9Im5vbmUiLz48cGF0aCBkPSJNIDcxNi44OCAzNzQgTCA3MDkuODggMzc3LjUgTCA3MDkuODggMzcwLjUgWiIgZmlsbD0iIzAwMDAwMCIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJub25lIi8+PGcgZmlsbD0iIzAwMDAwMCIgZm9udC1mYW1pbHk9IkhlbHZldGljYSIgdGV4dC1hbmNob3I9Im1pZGRsZSIgZm9udC1zaXplPSIxMXB4Ij48cmVjdCBmaWxsPSIjZmZmZmZmIiBzdHJva2U9Im5vbmUiIHg9IjUyMSIgeT0iMzU5IiB3aWR0aD0iMTg4IiBoZWlnaHQ9IjE0IiBzdHJva2Utd2lkdGg9IjAiLz48dGV4dCB4PSI2MTMuNSIgeT0iMzY3LjUiPmNhbkNvbm5lY3QoYnJva2VyQWRkcmVzcywgb3B0aW9ucyk8L3RleHQ+PC9nPjxwYXRoIGQ9Ik0gMjc1IDI4MSBMIDQyOCAyODEgTCA0NDIgMjk1IEwgNDQyIDMxMSBMIDI3NSAzMTEgTCAyNzUgMjgxIFoiIGZpbGw9IiNmNWY1ZjUiIHN0cm9rZT0iIzY2NjY2NiIgc3Ryb2tlLXdpZHRoPSIyIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJub25lIi8+PHBhdGggZD0iTSA0MjggMjgxIEwgNDI4IDI5NSBMIDQ0MiAyOTUiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzY2NjY2NiIgc3Ryb2tlLXdpZHRoPSIyIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJub25lIi8+PGcgZmlsbD0iIzAwMDAwMCIgZm9udC1mYW1pbHk9IkhlbHZldGljYSIgZm9udC1zaXplPSIxMXB4Ij48dGV4dCB4PSIyNzcuNSIgeT0iMjkyLjUiPk5vIHN0YXRpYyBjb25maWd1cmF0aW9uIGZvdW5kPC90ZXh0PjwvZz48cGF0aCBkPSJNIDQyOSAyODIgTCA0NzMuOTYgMjYxLjkxIiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgc3Ryb2tlLWRhc2hhcnJheT0iMyAzIiBwb2ludGVyLWV2ZW50cz0ibm9uZSIvPjxwYXRoIGQ9Ik0gNDcwLjAyIDI2Ny41MSBMIDQ3NC45OCAyNjEuNDYgTCA0NjcuMTYgMjYxLjEyIiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9Im5vbmUiLz48cmVjdCB4PSIzNSIgeT0iNTcwIiB3aWR0aD0iMTAiIGhlaWdodD0iMzAiIGZpbGw9IiMwMDAwMDAiIHN0cm9rZT0iIzAwMDAwMCIgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoMiwzKSIgb3BhY2l0eT0iMC4yNSIvPjxyZWN0IHg9IjM1IiB5PSI1NzAiIHdpZHRoPSIxMCIgaGVpZ2h0PSIzMCIgZmlsbD0iI2ZmZmZmZiIgc3Ryb2tlPSIjMDAwMDAwIiBwb2ludGVyLWV2ZW50cz0ibm9uZSIvPjxwYXRoIGQ9Ik0gNTAzIDUyMSBMIDI3OC4xMiA1MjEiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBzdHJva2UtZGFzaGFycmF5PSIzIDMiIHBvaW50ZXItZXZlbnRzPSJub25lIi8+PHBhdGggZD0iTSAyNzEuMTIgNTIxIEwgMjc4LjEyIDUxNy41IEwgMjc4LjEyIDUyNC41IFoiIGZpbGw9IiMwMDAwMDAiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0ibm9uZSIvPjxnIGZpbGw9IiMwMDAwMDAiIGZvbnQtZmFtaWx5PSJIZWx2ZXRpY2EiIGZvbnQtc3R5bGU9Iml0YWxpYyIgdGV4dC1hbmNob3I9Im1pZGRsZSIgZm9udC1zaXplPSIxMXB4Ij48cmVjdCBmaWxsPSIjZmZmZmZmIiBzdHJva2U9Im5vbmUiIHg9IjMyNCIgeT0iNTA2IiB3aWR0aD0iMTI1IiBoZWlnaHQ9IjE0IiBzdHJva2Utd2lkdGg9IjAiLz48dGV4dCB4PSIzODUuNSIgeT0iNTE0LjUiPmNvbmZpZ3VyYXRpb25fbm90X2ZvdW5kPC90ZXh0PjwvZz48cGF0aCBkPSJNIDI2NCA1NjkgTCA1My4xMiA1NjkuOTYiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0ibm9uZSIvPjxwYXRoIGQ9Ik0gNDYuMTIgNTY5Ljk5IEwgNTMuMSA1NjYuNDYgTCA1My4xMyA1NzMuNDYgWiIgZmlsbD0iIzAwMDAwMCIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJub25lIi8+PGcgZmlsbD0iIzAwMDAwMCIgZm9udC1mYW1pbHk9IkhlbHZldGljYSIgdGV4dC1hbmNob3I9Im1pZGRsZSIgZm9udC1zaXplPSIxMXB4Ij48cmVjdCBmaWxsPSIjZmZmZmZmIiBzdHJva2U9Im5vbmUiIHg9IjEwMSIgeT0iNTU0IiB3aWR0aD0iMTA3IiBoZWlnaHQ9IjE0IiBzdHJva2Utd2lkdGg9IjAiLz48dGV4dCB4PSIxNTMuNSIgeT0iNTYzIj5vbkNvbm5lY3Rpb25GYWlsdXJlPC90ZXh0PjwvZz48cGF0aCBkPSJNIDIwIDM1MCBMIDgwIDM1MCBMIDgwIDM2NSBMIDcwIDM4MCBMIDIwIDM4MCBaIiBmaWxsPSIjMzNmZmZmIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS13aWR0aD0iMiIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0ibm9uZSIvPjxwYXRoIGQ9Ik0gODAgMzUwIEwgODMxIDM1MCBMIDgzMSA2MzAgTCAyMCA2MzAgTCAyMCAzODAiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLXdpZHRoPSIyIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJub25lIi8+PGcgZmlsbD0iIzAwMDAwMCIgZm9udC1mYW1pbHk9IkhlbHZldGljYSIgdGV4dC1hbmNob3I9Im1pZGRsZSIgZm9udC1zaXplPSIxMXB4Ij48dGV4dCB4PSI1MC41IiB5PSIzNjkiPmFsdDwvdGV4dD48L2c+PGcgZmlsbD0iIzAwMDAwMCIgZm9udC1mYW1pbHk9IkhlbHZldGljYSIgZm9udC13ZWlnaHQ9ImJvbGQiIGZvbnQtc2l6ZT0iMTFweCI+PHRleHQgeD0iNDcuNSIgeT0iNDAzIj5bSG9vayByZXR1cm5zIFRydWVdPC90ZXh0PjwvZz48cGF0aCBkPSJNIDE4IDQ3MyBMIDgzMSA0NzMiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLXdpZHRoPSIyIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHN0cm9rZS1kYXNoYXJyYXk9IjYgNiIgcG9pbnRlci1ldmVudHM9Im5vbmUiLz48cmVjdCB4PSIyNjAiIHk9IjUyMCIgd2lkdGg9IjEwIiBoZWlnaHQ9IjUwIiBmaWxsPSIjZmZmZmZmIiBzdHJva2U9IiMwMDAwMDAiIHBvaW50ZXItZXZlbnRzPSJub25lIi8+PGcgZmlsbD0iIzAwMDAwMCIgZm9udC1mYW1pbHk9IkhlbHZldGljYSIgZm9udC13ZWlnaHQ9ImJvbGQiIGZvbnQtc2l6ZT0iMTFweCI+PHRleHQgeD0iNDcuNSIgeT0iNDg3LjUiPltIb29rIHJldHVybnMgbnVsbDwvdGV4dD48dGV4dCB4PSI0Ny41IiB5PSI1MDAuNSI+b3IgwqB0aHJvdyBIb29rRXhjZXB0aW9uXTwvdGV4dD48L2c+PHBhdGggZD0iTSA1MzAgNDMzIEwgNzU3IDQzMyBMIDc3MSA0NDcgTCA3NzEgNDYzIEwgNTMwIDQ2MyBMIDUzMCA0MzMgWiIgZmlsbD0iI2Y1ZjVmNSIgc3Ryb2tlPSIjNjY2NjY2IiBzdHJva2Utd2lkdGg9IjIiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9Im5vbmUiLz48cGF0aCBkPSJNIDc1NyA0MzMgTCA3NTcgNDQ3IEwgNzcxIDQ0NyIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjNjY2NjY2IiBzdHJva2Utd2lkdGg9IjIiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9Im5vbmUiLz48ZyBmaWxsPSIjMDAwMDAwIiBmb250LWZhbWlseT0iSGVsdmV0aWNhIiBmb250LXNpemU9IjExcHgiPjx0ZXh0IHg9IjUzMi41IiB5PSI0NDQuNSI+RnJvbSBub3cgb3duLCB0aGUgc2VxdWVuY2UgY29udGludWVzIGFzwqA8L3RleHQ+PHRleHQgeD0iNTMyLjUiIHk9IjQ1Ny41Ij5mb3IgQ29ubmVjdGlvbiBDcmVhdGlvbjwvdGV4dD48L2c+PC9nPjwvc3ZnPg==)

</div>

<div class="title">

Figure 13. Sequence diagram for a broker configuration provided by the
Hook

</div>

</div>

</div>

</div>

<div class="sect3">

#### 4.2.6. Authorizing Message Publishing {#hook_authorizing_publishing}

<div class="paragraph">

Any MQTT message sent from the client can be checked through the
`canPublish` method before being delivered to the target MQTT broker:

</div>

<div class="listingblock">

<div class="content">

``` {.CodeRay .highlight}
@Override
public boolean canPublish(String sessionId, String clientId, String brokerAddress,
  MqttMessage message) throws HookException {

  boolean canPublish = false;

  // Put here your authorization logic
    ...

  return canPublish;
}
```

</div>

</div>

<div class="paragraph">

The message contents can be inspected by looking at the `message`
parameter, which you could use to apply your own authorization logic.
See the
[`MqttMessage`](http://www.lightstreamer.com/api/mqtt.cool-hook-sdk/latest/cool/mqtt/hooks/MqttMessage.html)
API reference for more detailed information.

</div>

<div class="paragraph">

As an example, if your broker did not support QoS 2 messages, you might
prevent them from being sent; likewise, you could block all the messages
targeted to some specific topic names:

</div>

<div class="listingblock">

<div class="content">

``` {.CodeRay .highlight}
@Override
public boolean canPublish(String sessionId, String clientId, String brokerAddress,
  MqttMessage message) throws HookException {

  // Block QoS 2 messages
  if (QoS.EXACTLY_ONCE.equals(message.getQos())) {
    throw new HookException(301, "QoS 2 messages are NOT allowed");
  }

  // Block messages targeted to topic name starting with "$"
  if (message.getTopicName().startsWith("$")) {
    throw new HookException(302, "Message with topic name beginning with \"$\" are NOT allowed");
  }

  return true;
}
```

</div>

</div>

<div class="paragraph">

As anticipated in [Section 3.9.1, “Message Delivery
Notification”](#message_delivery_notifications), on the client side you
can leverage the
[`onMessageNotAuthorized`](http://www.lightstreamer.com/api/mqtt.cool-web-client/latest/MqttClient.html#onMessageNotAuthorized)
callback function to be informed about any authorization issue:

</div>

<div class="listingblock">

<div class="content">

``` {.CodeRay .highlight}
mqttClient.onMessageNotAuthorized = function(message, responseObject) {
  console.log('Publishing of message targeted to topic ' + message.destinationName +
    ' NOT authorized!');

  if (responseObject) {
    switch (responseObject.errorCode) {
      case 301:
        // Here the actions to be undertaken for handling the authorization issue due
        // to unsupported QoS 2 messages
        ...
        break;

      case 302:
        // Here the actions to be undertaken for handling the authorization issue due
        // to unsupported topic name
        ...
        break;
    }
  }
};
```

</div>

</div>

<div class="paragraph">

Once again, the `responseObject` parameter is provided only in case of
`HookException` thrown on the server side.

</div>

<div class="paragraph">

The diagram below shows an example of QoS 1 message publishing checked
by the Hook, where the activated connection type (shared or dedicated)
does not involve session persistence; therefore, on the client side the
message delivery notification occurs once the delivery protocol has been
completed on the server side.

</div>

<div class="imageblock" style="text-align: center">

<div class="content">

![can
publish](data:image/svg+xml;base64,PCFET0NUWVBFIHN2ZyBQVUJMSUMgIi0vL1czQy8vRFREIFNWRyAxLjEvL0VOIiAiaHR0cDovL3d3dy53My5vcmcvR3JhcGhpY3MvU1ZHLzEuMS9EVEQvc3ZnMTEuZHRkIj4KPHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHhtbG5zOnhsaW5rPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hsaW5rIiB3aWR0aD0iODExcHgiIGhlaWdodD0iNjQxcHgiIHZlcnNpb249IjEuMSIgc3R5bGU9ImJhY2tncm91bmQtY29sb3I6IHJnYigyNTUsIDI1NSwgMjU1KTsiPjxkZWZzLz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgwLjUsMC41KSI+PHBhdGggZD0iTSAyMjcgMTEzIEwgMzkxLjg4IDExMyIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJub25lIi8+PHBhdGggZD0iTSAzOTguODggMTEzIEwgMzkxLjg4IDExNi41IEwgMzkxLjg4IDEwOS41IFoiIGZpbGw9IiMwMDAwMDAiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0ibm9uZSIvPjxnIGZpbGw9IiMwMDAwMDAiIGZvbnQtZmFtaWx5PSJIZWx2ZXRpY2EiIGZvbnQtc3R5bGU9Iml0YWxpYyIgdGV4dC1hbmNob3I9Im1pZGRsZSIgZm9udC1zaXplPSIxMXB4Ij48cmVjdCBmaWxsPSIjZmZmZmZmIiBzdHJva2U9Im5vbmUiIHg9IjI0MyIgeT0iOTgiIHdpZHRoPSIxNDQiIGhlaWdodD0iMTQiIHN0cm9rZS13aWR0aD0iMCIvPjx0ZXh0IHg9IjMxMy41IiB5PSIxMDYuNSI+cHVibGlzaF9tZXNzYWdlKG1lc3NhZ2UpPC90ZXh0PjwvZz48cmVjdCB4PSIwIiB5PSIwIiB3aWR0aD0iODAiIGhlaWdodD0iNDAiIGZpbGw9IiNmZmYyY2MiIHN0cm9rZT0iIzAwMDAwMCIgcG9pbnRlci1ldmVudHM9Im5vbmUiLz48cGF0aCBkPSJNIDQwIDQwIEwgNDAgNjQwIiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgc3Ryb2tlLWRhc2hhcnJheT0iMyAzIiBwb2ludGVyLWV2ZW50cz0ibm9uZSIvPjxnIGZpbGw9IiMwMDAwMDAiIGZvbnQtZmFtaWx5PSJIZWx2ZXRpY2EiIGZvbnQtd2VpZ2h0PSJib2xkIiB0ZXh0LWFuY2hvcj0ibWlkZGxlIiBmb250LXNpemU9IjExcHgiPjx0ZXh0IHg9IjM5LjUiIHk9IjI0Ij46V2ViIENsaWVudDwvdGV4dD48L2c+PHJlY3QgeD0iMzUiIHk9IjkwIiB3aWR0aD0iMTAiIGhlaWdodD0iNjAiIGZpbGw9IiNmZmZmZmYiIHN0cm9rZT0iIzAwMDAwMCIgcG9pbnRlci1ldmVudHM9Im5vbmUiLz48cmVjdCB4PSIzNiIgeT0iNTQyIiB3aWR0aD0iMTAiIGhlaWdodD0iNTAiIGZpbGw9IiNmZmZmZmYiIHN0cm9rZT0iIzAwMDAwMCIgcG9pbnRlci1ldmVudHM9Im5vbmUiLz48cmVjdCB4PSIzNSIgeT0iMzYwIiB3aWR0aD0iMTAiIGhlaWdodD0iNTAiIGZpbGw9IiNmZmZmZmYiIHN0cm9rZT0iIzAwMDAwMCIgcG9pbnRlci1ldmVudHM9Im5vbmUiLz48cGF0aCBkPSJNIDQwMSAzMjAgTCAyMzAuMjQgMzIwIiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgc3Ryb2tlLWRhc2hhcnJheT0iMyAzIiBwb2ludGVyLWV2ZW50cz0ibm9uZSIvPjxwYXRoIGQ9Ik0gMjM4LjEyIDMxNS41IEwgMjI5LjEyIDMyMCBMIDIzOC4xMiAzMjQuNSIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJub25lIi8+PGcgZmlsbD0iIzAwMDAwMCIgZm9udC1mYW1pbHk9IkhlbHZldGljYSIgZm9udC1zdHlsZT0iaXRhbGljIiB0ZXh0LWFuY2hvcj0ibWlkZGxlIiBmb250LXNpemU9IjExcHgiPjxyZWN0IGZpbGw9IiNmZmZmZmYiIHN0cm9rZT0ibm9uZSIgeD0iMjUxIiB5PSIzMDUiIHdpZHRoPSIxMjciIGhlaWdodD0iMTQiIHN0cm9rZS13aWR0aD0iMCIvPjx0ZXh0IHg9IjMxMy41IiB5PSIzMTMuNSI+bWVzc2FnZV9hY2tub3dsZWRnZWQ8L3RleHQ+PC9nPjxyZWN0IHg9IjY0MSIgeT0iMCIgd2lkdGg9IjU5IiBoZWlnaHQ9IjQwIiBmaWxsPSIjZmZmMmNjIiBzdHJva2U9IiMwMDAwMDAiIHBvaW50ZXItZXZlbnRzPSJub25lIi8+PHBhdGggZD0iTSA2NzAuNSA0MCBMIDY3MC41IDY0MCIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHN0cm9rZS1kYXNoYXJyYXk9IjMgMyIgcG9pbnRlci1ldmVudHM9Im5vbmUiLz48ZyBmaWxsPSIjMDAwMDAwIiBmb250LWZhbWlseT0iSGVsdmV0aWNhIiBmb250LXdlaWdodD0iYm9sZCIgdGV4dC1hbmNob3I9Im1pZGRsZSIgZm9udC1zaXplPSIxMXB4Ij48dGV4dCB4PSI2NzAiIHk9IjI0Ij46SG9vazwvdGV4dD48L2c+PHJlY3QgeD0iNjY2IiB5PSIxNjAiIHdpZHRoPSIxMCIgaGVpZ2h0PSI1MCIgZmlsbD0iI2ZmZmZmZiIgc3Ryb2tlPSIjMDAwMDAwIiBwb2ludGVyLWV2ZW50cz0ibm9uZSIvPjxyZWN0IHg9IjczMCIgeT0iMCIgd2lkdGg9IjgwIiBoZWlnaHQ9IjQwIiBmaWxsPSIjZmZmMmNjIiBzdHJva2U9IiMwMDAwMDAiIHBvaW50ZXItZXZlbnRzPSJub25lIi8+PHBhdGggZD0iTSA3NzAgNDAgTCA3NzAgNjQwIiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgc3Ryb2tlLWRhc2hhcnJheT0iMyAzIiBwb2ludGVyLWV2ZW50cz0ibm9uZSIvPjxnIGZpbGw9IiMwMDAwMDAiIGZvbnQtZmFtaWx5PSJIZWx2ZXRpY2EiIGZvbnQtd2VpZ2h0PSJib2xkIiB0ZXh0LWFuY2hvcj0ibWlkZGxlIiBmb250LXNpemU9IjExcHgiPjx0ZXh0IHg9Ijc2OS41IiB5PSIyNCI+Ok1RVFQgQnJva2VyPC90ZXh0PjwvZz48cmVjdCB4PSI3NjUiIHk9IjI2MCIgd2lkdGg9IjEwIiBoZWlnaHQ9IjQwIiBmaWxsPSIjZmZmZmZmIiBzdHJva2U9IiMwMDAwMDAiIHBvaW50ZXItZXZlbnRzPSJub25lIi8+PHBhdGggZD0iTSA0MDUgMjYxIEwgNzU3Ljg4IDI2MSIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJub25lIi8+PHBhdGggZD0iTSA3NjQuODggMjYxIEwgNzU3Ljg4IDI2NC41IEwgNzU3Ljg4IDI1Ny41IFoiIGZpbGw9IiMwMDAwMDAiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0ibm9uZSIvPjxnIGZpbGw9IiMwMDAwMDAiIGZvbnQtZmFtaWx5PSJIZWx2ZXRpY2EiIGZvbnQtd2VpZ2h0PSJib2xkIiB0ZXh0LWFuY2hvcj0ibWlkZGxlIiBmb250LXNpemU9IjExcHgiPjxyZWN0IGZpbGw9IiNmZmZmZmYiIHN0cm9rZT0ibm9uZSIgeD0iNTYyIiB5PSIyNDYiIHdpZHRoPSI1MCIgaGVpZ2h0PSIxNCIgc3Ryb2tlLXdpZHRoPSIwIi8+PHRleHQgeD0iNTg1LjUiIHk9IjI1NC41Ij5QVUJMSVNIPC90ZXh0PjwvZz48cGF0aCBkPSJNIDc3MCAzMDAgTCA0MTMuMjQgMzAwIiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgc3Ryb2tlLWRhc2hhcnJheT0iMyAzIiBwb2ludGVyLWV2ZW50cz0ibm9uZSIvPjxwYXRoIGQ9Ik0gNDIxLjEyIDI5NS41IEwgNDEyLjEyIDMwMCBMIDQyMS4xMiAzMDQuNSIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJub25lIi8+PGcgZmlsbD0iIzAwMDAwMCIgZm9udC1mYW1pbHk9IkhlbHZldGljYSIgZm9udC13ZWlnaHQ9ImJvbGQiIHRleHQtYW5jaG9yPSJtaWRkbGUiIGZvbnQtc2l6ZT0iMTFweCI+PHJlY3QgZmlsbD0iI2ZmZmZmZiIgc3Ryb2tlPSJub25lIiB4PSI1NjYiIHk9IjI4NSIgd2lkdGg9IjQ5IiBoZWlnaHQ9IjE0IiBzdHJva2Utd2lkdGg9IjAiLz48dGV4dCB4PSI1ODkuNSIgeT0iMjkzLjUiPlBVQkFDSzwvdGV4dD48L2c+PHJlY3QgeD0iMzM5IiB5PSIwIiB3aWR0aD0iMTMzIiBoZWlnaHQ9IjQwIiBmaWxsPSIjZmZmMmNjIiBzdHJva2U9IiMwMDAwMDAiIHBvaW50ZXItZXZlbnRzPSJub25lIi8+PHBhdGggZD0iTSA0MDUuNSA0MCBMIDQwNS41IDY0MCIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHN0cm9rZS1kYXNoYXJyYXk9IjMgMyIgcG9pbnRlci1ldmVudHM9Im5vbmUiLz48ZyBmaWxsPSIjMDAwMDAwIiBmb250LWZhbWlseT0iSGVsdmV0aWNhIiBmb250LXdlaWdodD0iYm9sZCIgdGV4dC1hbmNob3I9Im1pZGRsZSIgZm9udC1zaXplPSIxMXB4Ij48dGV4dCB4PSI0MDUiIHk9IjI0Ij46TVFUVC5Db29sIFNlcnZlcjwvdGV4dD48L2c+PHJlY3QgeD0iNDAxIiB5PSIxMTEiIHdpZHRoPSIxMCIgaGVpZ2h0PSIzODMiIGZpbGw9IiNmZmZmZmYiIHN0cm9rZT0iIzAwMDAwMCIgcG9pbnRlci1ldmVudHM9Im5vbmUiLz48cmVjdCB4PSIxNjYiIHk9IjAiIHdpZHRoPSIxMTMiIGhlaWdodD0iNDAiIGZpbGw9IiNmZmYyY2MiIHN0cm9rZT0iIzAwMDAwMCIgcG9pbnRlci1ldmVudHM9Im5vbmUiLz48cGF0aCBkPSJNIDIyMi41IDQwIEwgMjIyLjUgNjQwIiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgc3Ryb2tlLWRhc2hhcnJheT0iMyAzIiBwb2ludGVyLWV2ZW50cz0ibm9uZSIvPjxnIGZpbGw9IiMwMDAwMDAiIGZvbnQtZmFtaWx5PSJIZWx2ZXRpY2EiIGZvbnQtd2VpZ2h0PSJib2xkIiB0ZXh0LWFuY2hvcj0ibWlkZGxlIiBmb250LXNpemU9IjExcHgiPjx0ZXh0IHg9IjIyMiIgeT0iMjQiPjpNcXR0Q2xpZW50PC90ZXh0PjwvZz48cmVjdCB4PSIyMTgiIHk9IjMyMCIgd2lkdGg9IjEwIiBoZWlnaHQ9IjQwIiBmaWxsPSIjZmZmZmZmIiBzdHJva2U9IiMwMDAwMDAiIHBvaW50ZXItZXZlbnRzPSJub25lIi8+PHBhdGggZD0iTSA0MDEgNDkyIEwgMjMwLjI0IDQ5MiIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHN0cm9rZS1kYXNoYXJyYXk9IjMgMyIgcG9pbnRlci1ldmVudHM9Im5vbmUiLz48cGF0aCBkPSJNIDIzOC4xMiA0ODcuNSBMIDIyOS4xMiA0OTIgTCAyMzguMTIgNDk2LjUiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0ibm9uZSIvPjxnIGZpbGw9IiMwMDAwMDAiIGZvbnQtZmFtaWx5PSJIZWx2ZXRpY2EiIGZvbnQtc3R5bGU9Iml0YWxpYyIgdGV4dC1hbmNob3I9Im1pZGRsZSIgZm9udC1zaXplPSIxMXB4Ij48cmVjdCBmaWxsPSIjZmZmZmZmIiBzdHJva2U9Im5vbmUiIHg9IjI2NSIgeT0iNDc3IiB3aWR0aD0iMTAwIiBoZWlnaHQ9IjE0IiBzdHJva2Utd2lkdGg9IjAiLz48dGV4dCB4PSIzMTMuNSIgeT0iNDg1LjUiPmF1dGhvcml6YXRpb25faXNzdWU8L3RleHQ+PC9nPjxyZWN0IHg9IjIxOCIgeT0iNDkyIiB3aWR0aD0iMTAiIGhlaWdodD0iNTAiIGZpbGw9IiNmZmZmZmYiIHN0cm9rZT0iIzAwMDAwMCIgcG9pbnRlci1ldmVudHM9Im5vbmUiLz48cmVjdCB4PSIyMTgiIHk9IjEwMCIgd2lkdGg9IjEwIiBoZWlnaHQ9IjUwIiBmaWxsPSIjZmZmZmZmIiBzdHJva2U9IiMwMDAwMDAiIHBvaW50ZXItZXZlbnRzPSJub25lIi8+PHBhdGggZD0iTSA0NSAxMDAgTCAyMDkuODggMTAwIiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9Im5vbmUiLz48cGF0aCBkPSJNIDIxNi44OCAxMDAgTCAyMDkuODggMTAzLjUgTCAyMDkuODggOTYuNSBaIiBmaWxsPSIjMDAwMDAwIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9Im5vbmUiLz48ZyBmaWxsPSIjMDAwMDAwIiBmb250LWZhbWlseT0iSGVsdmV0aWNhIiB0ZXh0LWFuY2hvcj0ibWlkZGxlIiBmb250LXNpemU9IjExcHgiPjxyZWN0IGZpbGw9IiNmZmZmZmYiIHN0cm9rZT0ibm9uZSIgeD0iOTMiIHk9Ijg1IiB3aWR0aD0iODAiIGhlaWdodD0iMTQiIHN0cm9rZS13aWR0aD0iMCIvPjx0ZXh0IHg9IjEzMS41IiB5PSI5My41Ij5zZW5kKG1lc3NhZ2UpPC90ZXh0PjwvZz48cGF0aCBkPSJNIDIxOCAxNDkgTCA0OC4yNCAxNDkuOTkiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBzdHJva2UtZGFzaGFycmF5PSIzIDMiIHBvaW50ZXItZXZlbnRzPSJub25lIi8+PHBhdGggZD0iTSA1Ni4wOSAxNDUuNDQgTCA0Ny4xMiAxNDkuOTkgTCA1Ni4xNCAxNTQuNDQiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0ibm9uZSIvPjxwYXRoIGQ9Ik0gNDExIDE2MCBMIDY1Ny44OCAxNjAiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0ibm9uZSIvPjxwYXRoIGQ9Ik0gNjY0Ljg4IDE2MCBMIDY1Ny44OCAxNjMuNSBMIDY1Ny44OCAxNTYuNSBaIiBmaWxsPSIjMDAwMDAwIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9Im5vbmUiLz48ZyBmaWxsPSIjMDAwMDAwIiBmb250LWZhbWlseT0iSGVsdmV0aWNhIiB0ZXh0LWFuY2hvcj0ibWlkZGxlIiBmb250LXNpemU9IjExcHgiPjxyZWN0IGZpbGw9IiNmZmZmZmYiIHN0cm9rZT0ibm9uZSIgeD0iNDQ0IiB5PSIxNDUiIHdpZHRoPSIxOTIiIGhlaWdodD0iMTQiIHN0cm9rZS13aWR0aD0iMCIvPjx0ZXh0IHg9IjUzOC41IiB5PSIxNTMuNSI+Y2FuUHVibGlzaChicm9rZXJBZGRyZXNzLCBtZXNzYWdlKTwvdGV4dD48L2c+PHBhdGggZD0iTSA2NzIgMjEwIEwgNDEzLjI0IDIxMCIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHN0cm9rZS1kYXNoYXJyYXk9IjMgMyIgcG9pbnRlci1ldmVudHM9Im5vbmUiLz48cGF0aCBkPSJNIDQyMS4xMiAyMDUuNSBMIDQxMi4xMiAyMTAgTCA0MjEuMTIgMjE0LjUiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0ibm9uZSIvPjxnIGZpbGw9IiMwMDAwMDAiIGZvbnQtZmFtaWx5PSJIZWx2ZXRpY2EiIHRleHQtYW5jaG9yPSJtaWRkbGUiIGZvbnQtc2l6ZT0iMTFweCI+PHJlY3QgZmlsbD0iI2ZmZmZmZiIgc3Ryb2tlPSJub25lIiB4PSI0MjgiIHk9IjE5NSIgd2lkdGg9IjIyNyIgaGVpZ2h0PSIxNCIgc3Ryb2tlLXdpZHRoPSIwIi8+PHRleHQgeD0iNTQwLjUiIHk9IjIwMy41Ij5yZXR1cm4gVHJ1ZSBvciBGYWxzZSBvciB0aHJvdyBIb29rRXhjZXB0aW9uPC90ZXh0PjwvZz48cGF0aCBkPSJNIDIxOCAzNjAgTCA1My4xMiAzNjAiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0ibm9uZSIvPjxwYXRoIGQ9Ik0gNDYuMTIgMzYwIEwgNTMuMTIgMzU2LjUgTCA1My4xMiAzNjMuNSBaIiBmaWxsPSIjMDAwMDAwIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9Im5vbmUiLz48ZyBmaWxsPSIjMDAwMDAwIiBmb250LWZhbWlseT0iSGVsdmV0aWNhIiB0ZXh0LWFuY2hvcj0ibWlkZGxlIiBmb250LXNpemU9IjExcHgiPjxyZWN0IGZpbGw9IiNmZmZmZmYiIHN0cm9rZT0ibm9uZSIgeD0iNzgiIHk9IjM0NSIgd2lkdGg9IjEwOCIgaGVpZ2h0PSIxNCIgc3Ryb2tlLXdpZHRoPSIwIi8+PHRleHQgeD0iMTMwLjUiIHk9IjM1My41Ij5vbk1lc3NhZ2VEZWxpdmVyZWQ8L3RleHQ+PC9nPjxwYXRoIGQ9Ik0gMjAgMjMwIEwgODAgMjMwIEwgODAgMjQ1IEwgNzAgMjYwIEwgMjAgMjYwIFoiIGZpbGw9IiMzM2ZmZmYiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLXdpZHRoPSIyIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJub25lIi8+PHBhdGggZD0iTSA4MCAyMzAgTCA3OTAgMjMwIEwgNzkwIDYzMCBMIDIwIDYzMCBMIDIwIDI2MCIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2Utd2lkdGg9IjIiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9Im5vbmUiLz48ZyBmaWxsPSIjMDAwMDAwIiBmb250LWZhbWlseT0iSGVsdmV0aWNhIiB0ZXh0LWFuY2hvcj0ibWlkZGxlIiBmb250LXNpemU9IjExcHgiPjx0ZXh0IHg9IjUwLjUiIHk9IjI0OSI+YWx0PC90ZXh0PjwvZz48cGF0aCBkPSJNIDIyIDQzMCBMIDc5MSA0MzAiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLXdpZHRoPSIyIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHN0cm9rZS1kYXNoYXJyYXk9IjYgNiIgcG9pbnRlci1ldmVudHM9Im5vbmUiLz48ZyBmaWxsPSIjMDAwMDAwIiBmb250LWZhbWlseT0iSGVsdmV0aWNhIiBmb250LXdlaWdodD0iYm9sZCIgZm9udC1zaXplPSIxMXB4Ij48dGV4dCB4PSI0Ny41IiB5PSIyODMiPltIb29rIHJldHVybnMgVHJ1ZV08L3RleHQ+PC9nPjxnIGZpbGw9IiMwMDAwMDAiIGZvbnQtZmFtaWx5PSJIZWx2ZXRpY2EiIGZvbnQtd2VpZ2h0PSJib2xkIiBmb250LXNpemU9IjExcHgiPjx0ZXh0IHg9IjQ3LjUiIHk9IjQ3Ni41Ij5bSG9vayByZXR1cm5zIEZhbHNlPC90ZXh0Pjx0ZXh0IHg9IjQ3LjUiIHk9IjQ4OS41Ij5vcsKgdGhyb3cgSG9va0V4Y2VwdGlvbl08L3RleHQ+PC9nPjxwYXRoIGQ9Ik0gMjIxIDU0MiBMIDU1LjEyIDU0Mi45NSIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJub25lIi8+PHBhdGggZD0iTSA0OC4xMiA1NDIuOTkgTCA1NS4xIDUzOS40NSBMIDU1LjE0IDU0Ni40NSBaIiBmaWxsPSIjMDAwMDAwIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9Im5vbmUiLz48ZyBmaWxsPSIjMDAwMDAwIiBmb250LWZhbWlseT0iSGVsdmV0aWNhIiB0ZXh0LWFuY2hvcj0ibWlkZGxlIiBmb250LXNpemU9IjExcHgiPjxyZWN0IGZpbGw9IiNmZmZmZmYiIHN0cm9rZT0ibm9uZSIgeD0iNjkiIHk9IjUyNyIgd2lkdGg9IjEzMiIgaGVpZ2h0PSIxNCIgc3Ryb2tlLXdpZHRoPSIwIi8+PHRleHQgeD0iMTMzLjUiIHk9IjUzNiI+b25NZXNzYWdlTm90QXV0aG9yaXplZDwvdGV4dD48L2c+PC9nPjwvc3ZnPg==)

</div>

<div class="title">

Figure 14. Sequence diagram for a QoS 1 message publishing

</div>

</div>

</div>

<div class="sect3">

#### 4.2.7. Authorizing Subscription {#hook_authorizing_subscription}

<div class="paragraph">

Similarly to the message publishing, any MQTT subscription can be
analyzed as well before being actually forwarded to the target MQTT
broker, by overriding the `canSubscribe` method:

</div>

<div class="listingblock">

<div class="content">

``` {.CodeRay .highlight}
@Override
public boolean canSubscribe(String sessionId, String clientId, String brokerAddress,
  MqttSubscription subscription) throws HookException {

  boolean canSubscribe = false;

  // Put here your authorization logic
  ...

  return canSubscribe;
}
```

</div>

</div>

<div class="paragraph">

In this case, the `subscription` parameter comes in handy to assist you
in deciding whether to proceed with the request. See the
[`MqttSubscription`](http://www.lightstreamer.com/api/mqtt.cool-hook-sdk/latest/cool/mqtt/hooks/MqttSubscription.html)
API reference for a complete description.

</div>

<div class="paragraph">

As a complementary example of the one proposed for the publishing case,
the following implementation disallows any subscription that requires
QoS 2, or which specifies a topic filter starting with a "\$":

</div>

<div class="listingblock">

<div class="content">

``` {.CodeRay .highlight}
@Override
public boolean canSubscribe(String sessionId, String clientId, String brokerAddress,
  MqttSubscription subscription) throws HookException {

  // Reject subscriptions with QoS 2
  if (QoS.EXACTLY_ONCE.equals(subscription.getQos())) {
    throw new HookException(401, "Subscription at QoS 2 are NOT allowed");
  }

  // Reject subscriptions to topic filter starting with "$"
  if (subscription.getTopicFilter().startsWith("$")) {
     throw new HookException(402, "Subscription to topic filters beginning with \"$\" are NOT allowed");
  }

  return true;
}
```

</div>

</div>

<div class="paragraph">

On the client side, the unauthorized subscription request will be
signaled through the
[`onSubscriptionNotAuthorized`](http://www.lightstreamer.com/api/mqtt.cool-web-client/latest/global.html#OnSubscriptionNotAuthorized)
callback function, as introduced in [Section 3.10.2, “Subscribe
Options”](#subscribe_options):

</div>

<div class="listingblock">

<div class="content">

``` {.CodeRay .highlight}
subscribeOptions.onSubscriptionNotAuthorized = function(responseObject) {
  console.log('Subscription NOT authorized!');

  if (responseObject) {
    switch (responseObject.errorCode) {
      case 401:
        // Here the actions to be undertaken for handling the authorization issue due
        // to rejected QoS 2 level
        ...
        break;

      case 402:
        // Here the actions to be undertaken for handling the authorization issue due
        // to rejected topic filter
        ...
        break;
    }
  }
};
```

</div>

</div>

<div class="paragraph">

As always, the `responseObject` parameter follows the same common
pattern for all Authorization Requests, as illustrated in the previous
sections.

</div>

<div class="paragraph">

In the diagram below, the sequence related to a subscription request
that goes through the Hook before being conveyed to the MQTT broker.

</div>

<div class="imageblock" style="text-align: center">

<div class="content">

![can
subscribe](data:image/svg+xml;base64,PCFET0NUWVBFIHN2ZyBQVUJMSUMgIi0vL1czQy8vRFREIFNWRyAxLjEvL0VOIiAiaHR0cDovL3d3dy53My5vcmcvR3JhcGhpY3MvU1ZHLzEuMS9EVEQvc3ZnMTEuZHRkIj4KPHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHhtbG5zOnhsaW5rPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hsaW5rIiB3aWR0aD0iODExcHgiIGhlaWdodD0iNjMxcHgiIHZlcnNpb249IjEuMSIgc3R5bGU9ImJhY2tncm91bmQtY29sb3I6IHJnYigyNTUsIDI1NSwgMjU1KTsiPjxkZWZzLz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgwLjUsMC41KSI+PHBhdGggZD0iTSAyMjggMTExIEwgMzkyLjg4IDExMSIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJub25lIi8+PHBhdGggZD0iTSAzOTkuODggMTExIEwgMzkyLjg4IDExNC41IEwgMzkyLjg4IDEwNy41IFoiIGZpbGw9IiMwMDAwMDAiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0ibm9uZSIvPjxnIGZpbGw9IiMwMDAwMDAiIGZvbnQtZmFtaWx5PSJIZWx2ZXRpY2EiIGZvbnQtc3R5bGU9Iml0YWxpYyIgdGV4dC1hbmNob3I9Im1pZGRsZSIgZm9udC1zaXplPSIxMXB4Ij48cmVjdCBmaWxsPSIjZmZmZmZmIiBzdHJva2U9Im5vbmUiIHg9IjI1MCIgeT0iOTYiIHdpZHRoPSIxMzIiIGhlaWdodD0iMTQiIHN0cm9rZS13aWR0aD0iMCIvPjx0ZXh0IHg9IjMxNC41IiB5PSIxMDQuNSI+c3Vic2NyaWJlKHRvcGljRmlsdGVyLCBxb3MpPC90ZXh0PjwvZz48cmVjdCB4PSIwIiB5PSIwIiB3aWR0aD0iODAiIGhlaWdodD0iNDAiIGZpbGw9IiNmZmYyY2MiIHN0cm9rZT0iIzAwMDAwMCIgcG9pbnRlci1ldmVudHM9Im5vbmUiLz48cGF0aCBkPSJNIDQwIDQwIEwgNDAgNjMwIiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgc3Ryb2tlLWRhc2hhcnJheT0iMyAzIiBwb2ludGVyLWV2ZW50cz0ibm9uZSIvPjxnIGZpbGw9IiMwMDAwMDAiIGZvbnQtZmFtaWx5PSJIZWx2ZXRpY2EiIGZvbnQtd2VpZ2h0PSJib2xkIiB0ZXh0LWFuY2hvcj0ibWlkZGxlIiBmb250LXNpemU9IjExcHgiPjx0ZXh0IHg9IjM5LjUiIHk9IjI0Ij46V2ViIENsaWVudDwvdGV4dD48L2c+PHJlY3QgeD0iMzUiIHk9Ijc4IiB3aWR0aD0iMTAiIGhlaWdodD0iNzIiIGZpbGw9IiNmZmZmZmYiIHN0cm9rZT0iIzAwMDAwMCIgcG9pbnRlci1ldmVudHM9Im5vbmUiLz48cmVjdCB4PSIzNSIgeT0iMzQ3IiB3aWR0aD0iMTAiIGhlaWdodD0iNDciIGZpbGw9IiNmZmZmZmYiIHN0cm9rZT0iIzAwMDAwMCIgcG9pbnRlci1ldmVudHM9Im5vbmUiLz48cGF0aCBkPSJNIDQwMSAzMDYgTCAyMzAuMjQgMzA2IiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgc3Ryb2tlLWRhc2hhcnJheT0iMyAzIiBwb2ludGVyLWV2ZW50cz0ibm9uZSIvPjxwYXRoIGQ9Ik0gMjM4LjEyIDMwMS41IEwgMjI5LjEyIDMwNiBMIDIzOC4xMiAzMTAuNSIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJub25lIi8+PGcgZmlsbD0iIzAwMDAwMCIgZm9udC1mYW1pbHk9IkhlbHZldGljYSIgZm9udC1zdHlsZT0iaXRhbGljIiB0ZXh0LWFuY2hvcj0ibWlkZGxlIiBmb250LXNpemU9IjExcHgiPjxyZWN0IGZpbGw9IiNmZmZmZmYiIHN0cm9rZT0ibm9uZSIgeD0iMjg2IiB5PSIyOTEiIHdpZHRoPSI1NyIgaGVpZ2h0PSIxNCIgc3Ryb2tlLXdpZHRoPSIwIi8+PHRleHQgeD0iMzEzLjUiIHk9IjI5OS41Ij5zdWJzY3JpYmVkPC90ZXh0PjwvZz48cmVjdCB4PSI2MzYiIHk9IjAiIHdpZHRoPSI1OSIgaGVpZ2h0PSI0MCIgZmlsbD0iI2ZmZjJjYyIgc3Ryb2tlPSIjMDAwMDAwIiBwb2ludGVyLWV2ZW50cz0ibm9uZSIvPjxwYXRoIGQ9Ik0gNjY1LjUgNDAgTCA2NjUuNSA2MzAiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBzdHJva2UtZGFzaGFycmF5PSIzIDMiIHBvaW50ZXItZXZlbnRzPSJub25lIi8+PGcgZmlsbD0iIzAwMDAwMCIgZm9udC1mYW1pbHk9IkhlbHZldGljYSIgZm9udC13ZWlnaHQ9ImJvbGQiIHRleHQtYW5jaG9yPSJtaWRkbGUiIGZvbnQtc2l6ZT0iMTFweCI+PHRleHQgeD0iNjY1IiB5PSIyNCI+Okhvb2s8L3RleHQ+PC9nPjxyZWN0IHg9IjY2MSIgeT0iMTYwIiB3aWR0aD0iMTAiIGhlaWdodD0iNTAiIGZpbGw9IiNmZmZmZmYiIHN0cm9rZT0iIzAwMDAwMCIgcG9pbnRlci1ldmVudHM9Im5vbmUiLz48cmVjdCB4PSI3MzAiIHk9IjAiIHdpZHRoPSI4MCIgaGVpZ2h0PSI0MCIgZmlsbD0iI2ZmZjJjYyIgc3Ryb2tlPSIjMDAwMDAwIiBwb2ludGVyLWV2ZW50cz0ibm9uZSIvPjxwYXRoIGQ9Ik0gNzcwIDQwIEwgNzcwIDYzMCIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHN0cm9rZS1kYXNoYXJyYXk9IjMgMyIgcG9pbnRlci1ldmVudHM9Im5vbmUiLz48ZyBmaWxsPSIjMDAwMDAwIiBmb250LWZhbWlseT0iSGVsdmV0aWNhIiBmb250LXdlaWdodD0iYm9sZCIgdGV4dC1hbmNob3I9Im1pZGRsZSIgZm9udC1zaXplPSIxMXB4Ij48dGV4dCB4PSI3NjkuNSIgeT0iMjQiPjpNUVRUIEJyb2tlcjwvdGV4dD48L2c+PHJlY3QgeD0iNzY1IiB5PSIyNjAiIHdpZHRoPSIxMCIgaGVpZ2h0PSIzMCIgZmlsbD0iI2ZmZmZmZiIgc3Ryb2tlPSIjMDAwMDAwIiBwb2ludGVyLWV2ZW50cz0ibm9uZSIvPjxwYXRoIGQ9Ik0gNDA1IDI2MSBMIDc1Ny44OCAyNjEiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0ibm9uZSIvPjxwYXRoIGQ9Ik0gNzY0Ljg4IDI2MSBMIDc1Ny44OCAyNjQuNSBMIDc1Ny44OCAyNTcuNSBaIiBmaWxsPSIjMDAwMDAwIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9Im5vbmUiLz48ZyBmaWxsPSIjMDAwMDAwIiBmb250LWZhbWlseT0iSGVsdmV0aWNhIiBmb250LXdlaWdodD0iYm9sZCIgdGV4dC1hbmNob3I9Im1pZGRsZSIgZm9udC1zaXplPSIxMXB4Ij48cmVjdCBmaWxsPSIjZmZmZmZmIiBzdHJva2U9Im5vbmUiIHg9IjU1MyIgeT0iMjQ2IiB3aWR0aD0iNjciIGhlaWdodD0iMTQiIHN0cm9rZS13aWR0aD0iMCIvPjx0ZXh0IHg9IjU4NS41IiB5PSIyNTQuNSI+U1VCU0NSSUJFPC90ZXh0PjwvZz48cGF0aCBkPSJNIDc2NyAyOTAgTCA0MTMuMjQgMjkwIiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgc3Ryb2tlLWRhc2hhcnJheT0iMyAzIiBwb2ludGVyLWV2ZW50cz0ibm9uZSIvPjxwYXRoIGQ9Ik0gNDIxLjEyIDI4NS41IEwgNDEyLjEyIDI5MCBMIDQyMS4xMiAyOTQuNSIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJub25lIi8+PGcgZmlsbD0iIzAwMDAwMCIgZm9udC1mYW1pbHk9IkhlbHZldGljYSIgZm9udC13ZWlnaHQ9ImJvbGQiIHRleHQtYW5jaG9yPSJtaWRkbGUiIGZvbnQtc2l6ZT0iMTFweCI+PHJlY3QgZmlsbD0iI2ZmZmZmZiIgc3Ryb2tlPSJub25lIiB4PSI1NjUiIHk9IjI3NSIgd2lkdGg9IjQ5IiBoZWlnaHQ9IjE0IiBzdHJva2Utd2lkdGg9IjAiLz48dGV4dCB4PSI1ODguNSIgeT0iMjgzLjUiPlNVQkFDSzwvdGV4dD48L2c+PHJlY3QgeD0iMzM5IiB5PSIwIiB3aWR0aD0iMTMzIiBoZWlnaHQ9IjQwIiBmaWxsPSIjZmZmMmNjIiBzdHJva2U9IiMwMDAwMDAiIHBvaW50ZXItZXZlbnRzPSJub25lIi8+PHBhdGggZD0iTSA0MDUuNSA0MCBMIDQwNS41IDYzMCIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHN0cm9rZS1kYXNoYXJyYXk9IjMgMyIgcG9pbnRlci1ldmVudHM9Im5vbmUiLz48ZyBmaWxsPSIjMDAwMDAwIiBmb250LWZhbWlseT0iSGVsdmV0aWNhIiBmb250LXdlaWdodD0iYm9sZCIgdGV4dC1hbmNob3I9Im1pZGRsZSIgZm9udC1zaXplPSIxMXB4Ij48dGV4dCB4PSI0MDUiIHk9IjI0Ij46TVFUVC5Db29sIFNlcnZlcjwvdGV4dD48L2c+PHJlY3QgeD0iNDAxIiB5PSIxMTAiIHdpZHRoPSIxMCIgaGVpZ2h0PSIzOTIiIGZpbGw9IiNmZmZmZmYiIHN0cm9rZT0iIzAwMDAwMCIgcG9pbnRlci1ldmVudHM9Im5vbmUiLz48cmVjdCB4PSIxNjYiIHk9IjAiIHdpZHRoPSIxMTMiIGhlaWdodD0iNDAiIGZpbGw9IiNmZmYyY2MiIHN0cm9rZT0iIzAwMDAwMCIgcG9pbnRlci1ldmVudHM9Im5vbmUiLz48cGF0aCBkPSJNIDIyMi41IDQwIEwgMjIyLjUgNjMwIiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgc3Ryb2tlLWRhc2hhcnJheT0iMyAzIiBwb2ludGVyLWV2ZW50cz0ibm9uZSIvPjxnIGZpbGw9IiMwMDAwMDAiIGZvbnQtZmFtaWx5PSJIZWx2ZXRpY2EiIGZvbnQtd2VpZ2h0PSJib2xkIiB0ZXh0LWFuY2hvcj0ibWlkZGxlIiBmb250LXNpemU9IjExcHgiPjx0ZXh0IHg9IjIyMiIgeT0iMjQiPjpNcXR0Q2xpZW50PC90ZXh0PjwvZz48cmVjdCB4PSIyMTgiIHk9IjMwNSIgd2lkdGg9IjEwIiBoZWlnaHQ9IjUwIiBmaWxsPSIjZmZmZmZmIiBzdHJva2U9IiMwMDAwMDAiIHBvaW50ZXItZXZlbnRzPSJub25lIi8+PHJlY3QgeD0iMjE4IiB5PSIxMDAiIHdpZHRoPSIxMCIgaGVpZ2h0PSI1MCIgZmlsbD0iI2ZmZmZmZiIgc3Ryb2tlPSIjMDAwMDAwIiBwb2ludGVyLWV2ZW50cz0ibm9uZSIvPjxyZWN0IHg9IjIxOSIgeT0iNTAwIiB3aWR0aD0iMTAiIGhlaWdodD0iNTAiIGZpbGw9IiNmZmZmZmYiIHN0cm9rZT0iIzAwMDAwMCIgcG9pbnRlci1ldmVudHM9Im5vbmUiLz48cGF0aCBkPSJNIDQ1IDEwMCBMIDIwOS44OCAxMDAiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0ibm9uZSIvPjxwYXRoIGQ9Ik0gMjE2Ljg4IDEwMCBMIDIwOS44OCAxMDMuNSBMIDIwOS44OCA5Ni41IFoiIGZpbGw9IiMwMDAwMDAiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0ibm9uZSIvPjxnIGZpbGw9IiMwMDAwMDAiIGZvbnQtZmFtaWx5PSJIZWx2ZXRpY2EiIHRleHQtYW5jaG9yPSJtaWRkbGUiIGZvbnQtc2l6ZT0iMTFweCI+PHJlY3QgZmlsbD0iI2ZmZmZmZiIgc3Ryb2tlPSJub25lIiB4PSI1OCIgeT0iODUiIHdpZHRoPSIxNTAiIGhlaWdodD0iMTQiIHN0cm9rZS13aWR0aD0iMCIvPjx0ZXh0IHg9IjEzMS41IiB5PSI5My41Ij5zdWJzY3JpYmUodG9waWNGaWx0ZXIsIG9wdGlvbnMpPC90ZXh0PjwvZz48cGF0aCBkPSJNIDIxOCAxNDkgTCA0OC4yNCAxNDkuOTkiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBzdHJva2UtZGFzaGFycmF5PSIzIDMiIHBvaW50ZXItZXZlbnRzPSJub25lIi8+PHBhdGggZD0iTSA1Ni4wOSAxNDUuNDQgTCA0Ny4xMiAxNDkuOTkgTCA1Ni4xNCAxNTQuNDQiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0ibm9uZSIvPjxwYXRoIGQ9Ik0gNDExIDE2MCBMIDY1Mi44OCAxNjAiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0ibm9uZSIvPjxwYXRoIGQ9Ik0gNjU5Ljg4IDE2MCBMIDY1Mi44OCAxNjMuNSBMIDY1Mi44OCAxNTYuNSBaIiBmaWxsPSIjMDAwMDAwIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9Im5vbmUiLz48ZyBmaWxsPSIjMDAwMDAwIiBmb250LWZhbWlseT0iSGVsdmV0aWNhIiB0ZXh0LWFuY2hvcj0ibWlkZGxlIiBmb250LXNpemU9IjExcHgiPjxyZWN0IGZpbGw9IiNmZmZmZmYiIHN0cm9rZT0ibm9uZSIgeD0iNDI3IiB5PSIxNDUiIHdpZHRoPSIyMjAiIGhlaWdodD0iMTQiIHN0cm9rZS13aWR0aD0iMCIvPjx0ZXh0IHg9IjUzNS41IiB5PSIxNTMuNSI+Y2FuU3Vic2NyaWJlKGJyb2tlckFkZHJlc3MsIHN1YnNjcmlwdGlvbik8L3RleHQ+PC9nPjxwYXRoIGQ9Ik0gNjY0IDIxMCBMIDQxMy4yNCAyMTAiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBzdHJva2UtZGFzaGFycmF5PSIzIDMiIHBvaW50ZXItZXZlbnRzPSJub25lIi8+PHBhdGggZD0iTSA0MjEuMTIgMjA1LjUgTCA0MTIuMTIgMjEwIEwgNDIxLjEyIDIxNC41IiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9Im5vbmUiLz48ZyBmaWxsPSIjMDAwMDAwIiBmb250LWZhbWlseT0iSGVsdmV0aWNhIiB0ZXh0LWFuY2hvcj0ibWlkZGxlIiBmb250LXNpemU9IjExcHgiPjxyZWN0IGZpbGw9IiNmZmZmZmYiIHN0cm9rZT0ibm9uZSIgeD0iNDI0IiB5PSIxOTUiIHdpZHRoPSIyMjciIGhlaWdodD0iMTQiIHN0cm9rZS13aWR0aD0iMCIvPjx0ZXh0IHg9IjUzNi41IiB5PSIyMDMuNSI+cmV0dXJuIFRydWUgb3IgRmFsc2Ugb3IgdGhyb3cgSG9va0V4Y2VwdGlvbjwvdGV4dD48L2c+PHBhdGggZD0iTSAyMTYgMzQ3IEwgNTIuMTIgMzQ3IiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9Im5vbmUiLz48cGF0aCBkPSJNIDQ1LjEyIDM0NyBMIDUyLjEyIDM0My41IEwgNTIuMTIgMzUwLjUgWiIgZmlsbD0iIzAwMDAwMCIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJub25lIi8+PGcgZmlsbD0iIzAwMDAwMCIgZm9udC1mYW1pbHk9IkhlbHZldGljYSIgdGV4dC1hbmNob3I9Im1pZGRsZSIgZm9udC1zaXplPSIxMXB4Ij48cmVjdCBmaWxsPSIjZmZmZmZmIiBzdHJva2U9Im5vbmUiIHg9IjcxIiB5PSIzMzIiIHdpZHRoPSIxMjAiIGhlaWdodD0iMTQiIHN0cm9rZS13aWR0aD0iMCIvPjx0ZXh0IHg9IjEyOS41IiB5PSIzNDAuNSI+b25TdWJzY3JpcHRpb25TdWNjZXNzPC90ZXh0PjwvZz48cGF0aCBkPSJNIDIwIDIzMCBMIDgwIDIzMCBMIDgwIDI0NSBMIDcwIDI2MCBMIDIwIDI2MCBaIiBmaWxsPSIjMzNmZmZmIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS13aWR0aD0iMiIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0ibm9uZSIvPjxwYXRoIGQ9Ik0gODAgMjMwIEwgNzkwIDIzMCBMIDc5MCA2MjAgTCAyMCA2MjAgTCAyMCAyNjAiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLXdpZHRoPSIyIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJub25lIi8+PGcgZmlsbD0iIzAwMDAwMCIgZm9udC1mYW1pbHk9IkhlbHZldGljYSIgdGV4dC1hbmNob3I9Im1pZGRsZSIgZm9udC1zaXplPSIxMXB4Ij48dGV4dCB4PSI1MC41IiB5PSIyNDkiPmFsdDwvdGV4dD48L2c+PHBhdGggZD0iTSAyMiA0MzAgTCA3OTEgNDMwIiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS13aWR0aD0iMiIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBzdHJva2UtZGFzaGFycmF5PSI2IDYiIHBvaW50ZXItZXZlbnRzPSJub25lIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoNDcuNSwyNzQuNSkiPjxzd2l0Y2g+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OnZpc2libGU7IiBwb2ludGVyLWV2ZW50cz0iYWxsIiB3aWR0aD0iMTAyIiBoZWlnaHQ9IjExIiByZXF1aXJlZEZlYXR1cmVzPSJodHRwOi8vd3d3LnczLm9yZy9UUi9TVkcxMS9mZWF0dXJlI0V4dGVuc2liaWxpdHkiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTFweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6IHJnYigwLCAwLCAwKTsgbGluZS1oZWlnaHQ6IDEuMjsgdmVydGljYWwtYWxpZ246IHRvcDsgd2lkdGg6IDEwM3B4OyB3aGl0ZS1zcGFjZTogbm93cmFwOyB3b3JkLXdyYXA6IG5vcm1hbDsgZm9udC13ZWlnaHQ6IGJvbGQ7Ij48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTppbmxpbmUtYmxvY2s7dGV4dC1hbGlnbjppbmhlcml0O3RleHQtZGVjb3JhdGlvbjppbmhlcml0OyI+W0hvb2sgcmV0dXJucyBUcnVlXTwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48dGV4dCB4PSI1MSIgeT0iMTEiIGZpbGw9IiMwMDAwMDAiIHRleHQtYW5jaG9yPSJtaWRkbGUiIGZvbnQtc2l6ZT0iMTFweCIgZm9udC1mYW1pbHk9IkhlbHZldGljYSIgZm9udC13ZWlnaHQ9ImJvbGQiPltIb29rIHJldHVybnMgVHJ1ZV08L3RleHQ+PC9zd2l0Y2g+PC9nPjxnIGZpbGw9IiMwMDAwMDAiIGZvbnQtZmFtaWx5PSJIZWx2ZXRpY2EiIGZvbnQtd2VpZ2h0PSJib2xkIiBmb250LXNpemU9IjExcHgiPjx0ZXh0IHg9IjQ3LjUiIHk9IjQ3Ni41Ij5bSG9vayByZXR1cm5zIEZhbHNlPC90ZXh0Pjx0ZXh0IHg9IjQ3LjUiIHk9IjQ4OS41Ij5vcsKgdGhyb3cgSG9va0V4Y2VwdGlvbl08L3RleHQ+PC9nPjxwYXRoIGQ9Ik0gNDA2IDUwMiBMIDIzMS4yNCA1MDEuMDEiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBzdHJva2UtZGFzaGFycmF5PSIzIDMiIHBvaW50ZXItZXZlbnRzPSJub25lIi8+PHBhdGggZD0iTSAyMzkuMTQgNDk2LjU2IEwgMjMwLjEyIDUwMS4wMSBMIDIzOS4wOSA1MDUuNTYiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0ibm9uZSIvPjxnIGZpbGw9IiMwMDAwMDAiIGZvbnQtZmFtaWx5PSJIZWx2ZXRpY2EiIGZvbnQtc3R5bGU9Iml0YWxpYyIgdGV4dC1hbmNob3I9Im1pZGRsZSIgZm9udC1zaXplPSIxMXB4Ij48cmVjdCBmaWxsPSIjZmZmZmZmIiBzdHJva2U9Im5vbmUiIHg9IjI2OCIgeT0iNDg2IiB3aWR0aD0iMTAwIiBoZWlnaHQ9IjE0IiBzdHJva2Utd2lkdGg9IjAiLz48dGV4dCB4PSIzMTYuNSIgeT0iNDk1Ij5hdXRob3JpemF0aW9uX2lzc3VlPC90ZXh0PjwvZz48cmVjdCB4PSIzNSIgeT0iNTUwIiB3aWR0aD0iMTAiIGhlaWdodD0iMzIiIGZpbGw9IiNmZmZmZmYiIHN0cm9rZT0iIzAwMDAwMCIgcG9pbnRlci1ldmVudHM9Im5vbmUiLz48cGF0aCBkPSJNIDIyMyA1NTAgTCA1MS4xMiA1NTAiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0ibm9uZSIvPjxwYXRoIGQ9Ik0gNDQuMTIgNTUwIEwgNTEuMTIgNTQ2LjUgTCA1MS4xMiA1NTMuNSBaIiBmaWxsPSIjMDAwMDAwIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9Im5vbmUiLz48ZyBmaWxsPSIjMDAwMDAwIiBmb250LWZhbWlseT0iSGVsdmV0aWNhIiB0ZXh0LWFuY2hvcj0ibWlkZGxlIiBmb250LXNpemU9IjExcHgiPjxyZWN0IGZpbGw9IiNmZmZmZmYiIHN0cm9rZT0ibm9uZSIgeD0iNTkiIHk9IjUzNSIgd2lkdGg9IjE0OSIgaGVpZ2h0PSIxNCIgc3Ryb2tlLXdpZHRoPSIwIi8+PHRleHQgeD0iMTMyLjUiIHk9IjU0My41Ij5vblN1YnNjcmlwdGlvbk5vdEF1dGhvcml6ZWQ8L3RleHQ+PC9nPjwvZz48L3N2Zz4=)

</div>

<div class="title">

Figure 15. Sequence diagram for a subscription

</div>

</div>

</div>

<div class="sect3">

#### 4.2.8. Notifying of Session Closing, Disconnection and Unsubscription {#_notifying_of_session_closing_disconnection_and_unsubscription}

<div class="paragraph">

Let’s finish this chapter on the Hook development with a quick overview
of the so-called *Simple Notifications* methods, which are invoked when
long-term activities like sessions, connections, and subscriptions
complete their own life cycle.

</div>

<div class="paragraph">

For example, a session opened against MQTT.Cool could end either because
of an explicit request made by the client or due to any network issue;
in such case, the `onSessionClose` method is invoked, therefore you
could override it to apply your own cleanup logic, if any:

</div>

<div class="listingblock">

<div class="content">

``` {.CodeRay .highlight}
@Override
public void onSessionClose(String sessionId) {
  // Put here your cleanup logic
  ...
}
```

</div>

</div>

<div class="paragraph">

Similarly, a connection established with any MQTT broker may be
explicitly closed by the originating client (see [Section 3.13,
“Disconnecting”](#disconnecting)); you will be informed of this event
through `onDisconnection`:

</div>

<div class="listingblock">

<div class="content">

``` {.CodeRay .highlight}
@Override
public void onDisconnection(String sessionId, String clientId, String brokerAddress) {
  // Put here your actions
  ...
}
```

</div>

</div>

<div class="admonitionblock warning">

  ---- ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  **   `onDisconnection` is also invoked because of session interruption while the client is currently connected: if it is the case, both `onSessionClose` and `onDisconnection` will be triggered.
  ---- ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

</div>

<div class="paragraph">

Lastly, a currently active subscription may be terminated by an
unsubscription request (see [Section 3.11,
“Unsubscribing”](#unsubscribing)), which will be reported by the
`onUnsubscribe` method:

</div>

<div class="listingblock">

<div class="content">

``` {.CodeRay .highlight}
@Override
public void onUnsubscribe(String sessionId, String clientId, String brokerAddress,
  String topicFilter) {

  // Put here your actions
  ...
}
```

</div>

</div>

</div>

</div>

<div class="sect2">

### 4.3. Packaging, Configuration and Deployment {#_packaging_configuration_and_deployment}

<div class="paragraph">

To deploy your custom Hook into the MQTT.Cool installation, you need to
perform the following steps:

</div>

<div class="olist arabic">

1.  Build the Hook by executing the Maven `package` goal from your
    project folder:

    <div class="listingblock">

    <div class="content">

    ``` {.CodeRay .highlight}
    $ mvn package
    ```

    </div>

    </div>

2.  Locate the jar file (which should be in the `target` folder) and
    drop it into into the `<MQTT.COOL_HOME>/mqtt_connectors/lib` folder.

3.  Edit
    `<MQTT.COOL_HOME>/mqtt_connectors/mqtt_master_connector_conf.xml`,
    by adding the fully qualified Hook class name into the
    `<param name="hook" …​ />` tag, right before `<master_connector>`:

    <div class="listingblock">

    <div class="content">

    ``` {.CodeRay .highlight}
    <mqtt_master_connector_conf>
      ...
      <param name="hook">my.cool.hook.MyCoolHook</param>

      <master_connector>
      ...
    ```

    </div>

    </div>

    <div class="admonitionblock tip">

    +-----------------------------------+-----------------------------------+
    | **                                | <div class="paragraph">           |
    |                                   |                                   |
    |                                   | Alternatively, you might want to  |
    |                                   | uncomment and replace the         |
    |                                   | provided factory example:         |
    |                                   |                                   |
    |                                   | </div>                            |
    |                                   |                                   |
    |                                   | <div class="listingblock">        |
    |                                   |                                   |
    |                                   | <div class="content">             |
    |                                   |                                   |
    |                                   | ``` {.CodeRay .highlight}         |
    |                                   | <!-- Optional. Fully qualified cl |
    |                                   | ass name of a hook with purpose o |
    |                                   | f                                 |
    |                                   |      authentication and authoriza |
    |                                   | tion of users. Must implement the |
    |                                   |      MQTTCoolHook interface.      |
    |                                   |      See docs for more informatio |
    |                                   | n. -->                            |
    |                                   | <!--                              |
    |                                   | <param name="hook">my.package.Hoo |
    |                                   | k</param>                         |
    |                                   | -->                               |
    |                                   | ```                               |
    |                                   |                                   |
    |                                   | </div>                            |
    |                                   |                                   |
    |                                   | </div>                            |
    +-----------------------------------+-----------------------------------+

    </div>

4.  Start MQTT.Cool and look into the
    `<MQTT.COOL_HOME>/log/mqtt.cool.log` file for any possible issue.

    <div class="paragraph">

    If deployment went well, you should get a log line like this at
    startup:

    </div>

    <div class="listingblock">

    <div class="content">

        ...
        04-apr-17 12:06:34,136|INFO|MQTTCoolLogger.init     |Init for MQTT      |Hook initialized with FQN my.cool.hook.MyCoolHook
        ...

    </div>

    </div>

</div>

</div>

</div>

</div>

<div class="sect1">

Appendix A: Connection Parameters {#_connection_parameters}
---------------------------------

<div class="sectionbody">

<div class="paragraph">

The following is the complete list of the supported connection
parameters that can be configured in the
`<MQTT.COOL_HOME>/mqtt_connector/mqtt_master_connector_conf.xml` file.

</div>

<div class="admonitionblock tip">

  ---- --------------------------------------------------------------------------------------
  **   The details below are similar to the inline documentation provided in the same file.
  ---- --------------------------------------------------------------------------------------

</div>

<div class="dlist">

&lt;connection\_alias&gt;.server\_address

:   (Mandatory). The address of the MQTT broker to connect to. Accepted
    URI forms are:

    <div class="ulist">

    -   `tcp://<host>:<port>`

    -   `mqtt://<host>:<port>`

    </div>

    <div class="paragraph">

    Example:

    </div>

</div>

<div class="listingblock">

<div class="content">

``` {.CodeRay .highlight}
<param name="mosquitto.server_address">tcp://localhost:1883</param>
```

</div>

</div>

<div class="dlist">

&lt;connection\_alias&gt;.clientid\_prefix

:   (Optional). Client Id prefix to be used for shared connections. If
    the clients want to share a single connection (see [Section 3.6.3,
    “Shared End-to-End Connection”](#shared_connection)), a randomly
    generated suffix will be appended in order to generate a unique
    ClientId, for opening the physical connection toward the MQTT
    broker. Uniqueness of the ClientId is mandatory as multiple shared
    connections may exist for the same broker.

    <div class="paragraph">

    Default value: `MQTT_Cool`.

    </div>

    <div class="paragraph">

    Example:

    </div>

    <div class="listingblock">

    <div class="content">

    ``` {.CodeRay .highlight}
    <param name="mosquitto.clientid_prefix">mosquitto_client</param>
    ```

    </div>

    </div>

&lt;connection\_alias&gt;.connection\_timeout

:   (Optional). The connection timeout expressed in seconds.

    <div class="paragraph">

    Default value: `5`.

    </div>

    <div class="paragraph">

    Example:

    </div>

    <div class="listingblock">

    <div class="content">

    ``` {.CodeRay .highlight}
    <param name="mosquitto.connection_timeout">30</param>
    ```

    </div>

    </div>

&lt;connection\_alias&gt;.keep\_alive

:   (Optional). The keep alive interval expressed in seconds.

    <div class="paragraph">

    Default value: `30`

    </div>

    <div class="paragraph">

    Example:

    </div>

    <div class="listingblock">

    <div class="content">

    ``` {.CodeRay .highlight}
    <param name="mosquitto.keep_alive">10</param>
    ```

    </div>

    </div>

&lt;connection\_alias&gt;.username

:   (Optional). The username for authenticating with the MQTT broker.
    The value which may be provided by the client will take precedence
    over this setting.

    <div class="paragraph">

    Example:

    </div>

    <div class="listingblock">

    <div class="content">

    ``` {.CodeRay .highlight}
    <param name="mosquitto.username">username</param>
    ```

    </div>

    </div>

&lt;connection\_alias&gt;.password

:   (Optional). The password for authenticating with the MQTT broker.
    The value which may be provided by the client will take precedence
    over this setting.

    <div class="paragraph">

    Example:

    </div>

    <div class="listingblock">

    <div class="content">

    ``` {.CodeRay .highlight}
    <param name="mosquitto.username">username</param>
    ```

    </div>

    </div>

&lt;connection\_alias&gt;.will\_message

:   (Optional). The payload of the Will Message, which is interpreted on
    the basis of the `will_message_format` parameter. The Will Message
    and related parameters (as defined below) are processed only in the
    case of dedicated connections. The Will Message and related
    parameters which may be provided by the client will take precedence
    over the corresponding settings.

    <div class="paragraph">

    Example:

    </div>

    <div class="listingblock">

    <div class="content">

    ``` {.CodeRay .highlight}
    <param name="mosquitto.will_message">will_message</param>
    ```

    </div>

    </div>

&lt;connection\_alias&gt;.will\_message\_format

:   (Optional). As the `CONNECT` Control Packet will contain just a
    sequence of raw bytes for the Will Message, this setting specifies
    how to interpret the payload provided through the `will_message`
    parameter, in order to give the opportunity to supply either a
    string or a binary sequence.

    <div class="paragraph">

    Specify:

    </div>

    <div class="ulist">

    -   `UTF-8`, to interpret the text as a regular string, which will
        be then be encoded into the final sequence of bytes using the
        UTF-8 character set.

    -   `base64`, to interpret the text as a *Base64* encoded string,
        which will be then decoded accordingly to make the final
        sequence of bytes.

    </div>

    <div class="paragraph">

    Default value: `UTF-8`.

    </div>

</div>

<div class="paragraph">

Example:

</div>

<div class="listingblock">

<div class="content">

``` {.CodeRay .highlight}
<param name="mosquitto.will_message_format">base64</param>
```

</div>

</div>

<div class="dlist">

&lt;connection\_alias&gt;.will\_topic

:   (Mandatory if "will\_message" is defined). The topic name of the
    Will Message. Must be at least 1 character in length.

    <div class="paragraph">

    Example:

    </div>

    <div class="listingblock">

    <div class="content">

    ``` {.CodeRay .highlight}
    <param name="mosquitto.will_topic">will_topic</param>
    ```

    </div>

    </div>

&lt;connection\_alias&gt;.will\_qos

:   (Optional, but considered only if `will_message` is defined). The
    QoS integer value of the Will Message.

    <div class="paragraph">

    Default value: `0`.

    </div>

    <div class="paragraph">

    Example:

    </div>

    <div class="listingblock">

    <div class="content">

    ``` {.CodeRay .highlight}
    <param name="mosquitto.will_qos">1</param>
    ```

    </div>

    </div>

&lt;connection\_alias&gt;.will\_retain

:   (Optional, but considered only if `will_message` is defined). The
    retain flag of the Will Message.

    <div class="paragraph">

    Default value: `false`.

    </div>

    <div class="paragraph">

    Example:

    </div>

    <div class="listingblock">

    <div class="content">

    ``` {.CodeRay .highlight}
    <param name="mosquitto.will_retain">true</param>
    ```

    </div>

    </div>

</div>

</div>

</div>

<div class="sect1">

Appendix B: Access the Lightstreamer Client API {#_access_the_lightstreamer_client_api}
-----------------------------------------------

<div class="sectionbody">

<div class="paragraph">

In this appendix, we will give you a short introduction on how to access
the Lightstreamer Client API (on which the MQTT.Cool library is based)
in order to exploit the features offered by the embedded Lightstreamer
Engine.

</div>

<div class="paragraph">

For more in-depth details on the API and Lightstreamer client
development, see:

</div>

<div class="ulist">

-   [Web Client Unified API
    Reference](https://www.lightstreamer.com/docs/client_javascript_uni_api/index.html)

-   [Web Client
    Development](https://www.lightstreamer.com/docs/client_javascript_base/Web%20Client%20Guide.pdf)

</div>

<div class="sect2">

### B.1. The LightstreamerClient Object {#_the_lightstreamerclient_object}

<div class="paragraph">

In [Section 3.5, “The MQTTCoolSession Interface”](#session_interface),
we have briefly mentioned the
[`onLsClient`](http://www.lightstreamer.com/api/mqtt.cool-web-client/latest/MQTTCoolListener.html#onLsClient)
event, which is invoked when a new *Lightstreamer Session* is available,
just before connecting to the MQTT.Cool server.

</div>

<div class="paragraph">

The Session is provided through the `lsClient` parameter, which
represents an instance of
[`LightstreamerClient`](http://www.lightstreamer.com/api/ls-web-client/7.0.4/LightstreamerClient.html).
Being the entry point of the Lightstreamer JavaScript Client API, this
objects could be considered as the *bridge* between the two APIs.

</div>

<div class="paragraph">

In the subsequent sections, you will be provided with some tips on
several potential uses of this object and related entities.

</div>

<div class="sect3">

#### B.1.1. Managing the Connection Options {#_managing_the_connection_options}

<div class="paragraph">

The provided `LightstreamerClient` instance is already configured and
initialized to be used by the MQTT.Cool library for establishing the
connection towards the target MQTT.Cool server.

</div>

<div class="paragraph">

However, you have the opportunity to manage the attached
[`ConnectionOptions`](http://www.lightstreamer.com/api/ls-web-client/7.0.4/ConnectionOptions.html)
instance to set specific connection properties as per your need.

</div>

<div class="admonitionblock warning">

  ---- -----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  **   Changes made to the `ConnectionOptions` object will affect only the connection established between the client and the MQTT.Cool server. The connection parameters relative to MQTT brokers have been already discussed in [Chapter 2, *Addressing MQTT Brokers*](#_addressing_mqtt_brokers) and [Appendix A, *Connection Parameters*](#_connection_parameters).
  ---- -----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

</div>

<div class="paragraph">

For example, you might want to change default values for properties
related to possible timeouts, like the following:

</div>

<div class="ulist">

-   [`connectTimeout`](http://www.lightstreamer.com/api/ls-web-client/7.0.4/ConnectionOptions.html#setConnectTimeout)

-   [`keepaliveInterval`](http://www.lightstreamer.com/api/ls-web-client/7.0.4/ConnectionOptions.html#setKeepaliveInterval)

-   [`idleTimeout`](http://www.lightstreamer.com/api/ls-web-client/7.0.4/ConnectionOptions.html#setIdleTimeout)

-   [`reconnectTimeout`](http://www.lightstreamer.com/api/ls-web-client/7.0.4/ConnectionOptions.html#setReconnectTimeout)

</div>

<div class="paragraph">

and so on.

</div>

<div class="paragraph">

Similarly, through
[setForcedTransport](http://www.lightstreamer.com/api/ls-web-client/7.0.4/ConnectionOptions.html#setForcedTransport)
method you could *force* a fixed transport (for example, HTTP only),
disabling the native *Stream-Sense* algorithm.

</div>

<div class="paragraph">

See the
[`ConnectionOptions`](http://www.lightstreamer.com/api/ls-web-client/7.0.4/ConnectionOptions.html)
API Reference for the complete list of modifiable properties.

</div>

<div class="paragraph">

As already said, `onLsClient` is the expected place where to apply any
change to the connection just before it is actually established. We are
now ready to complete the main connection pattern extension started
[here](#main_connection_pattern_ext):

</div>

<div class="listingblock">

<div class="content">

``` {.CodeRay .highlight}
mqttcool.openSession(..., {

  onLsClient: function(lsClient) {
    // Get the attached ConnectOptions object
    var connectOptions = lsClient.connectionOptions;

    // Apply the required changes
    connectOptions.setConnectTimeout(10);
    connectOptions.setKeepaliveInterval(30);

    ...
  },

  ...
});
```

</div>

</div>

</div>

</div>

<div class="sect2">

### B.2. Bandwidth Throttling {#_bandwidth_throttling}

<div class="paragraph">

In [Section 3.10.2.3, “Frequency Management”](#_frequency_management) we
have seen how MQTT.Cool allows specifying the rate at which messages can
arrive for a specific MQTT topic. In addition, the underlying
Lightstreamer Engine permits to go beyond that: you can also specify the
maximum bandwidth allowed for all messages routed by the MQTT.Cool
server for this specific session.

</div>

<div class="paragraph">

Once more, `ConnectionOptions` exposes the needed
[setMaxBandwidth](http://www.lightstreamer.com/api/ls-web-client/7.0.4/ConnectionOptions.html#setMaxBandwidth)
method that allows you to do the magic:

</div>

<div class="listingblock">

<div class="content">

``` {.CodeRay .highlight}
mqttcool.openSession(..., {

  onLsClient: function(lsClient) {
    // Get the attached ConnectOptions object
    var connectOptions = lsClient.connectionOptions;

    // Request to consume up to 300 kbps
    connectOptions.setMaxBandwidth(300);
    ...
  },

  ...
});
```

</div>

</div>

<div class="admonitionblock tip">

  ---- --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  **   The [Hello IoT World](https://github.com/MQTTCool/MQTT.Cool-example-Hello_IoT_World-client-javascript) example available on GitHub employs the same technique to issue a new max bandwidth request according to the movements on the slider, as shown in [index.js](https://github.com/MQTTCool/MQTT.Cool-example-Hello_IoT_World-client-javascript/blob/master/src/web/js/index.js) (line 112).
  ---- --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

</div>

</div>

<div class="sect2">

### B.3. Attaching a Listener {#_attaching_a_listener}

<div class="paragraph">

If you are are interested in being notified about low-level connection
activities and errors, you could add a `ClientListener` instance to
`LightstreamerClient`:

</div>

<div class="listingblock">

<div class="content">

``` {.CodeRay .highlight}
mqttcool.openSession(..., {

  onLsClient: function(lsClient) {
    // Addd a listener to the LightstreamerClient object
    lsClient.addListener({

      onListenerStart: function { },

      onListenerEnd: function { },

      onPropertyChange: function { },

      onServerError: function { },

      onShareAbort: function { },

      onStatusChange: function { }
    });
    ...
  },

  ...
});
```

</div>

</div>

<div class="paragraph">

See the
[`ClientListener`](http://www.lightstreamer.com/api/ls-web-client/7.0.4/ClientListener.html)
API Reference to get detailed documentation for every event.

</div>

</div>

<div class="sect2">

### B.4. Private Operations {#_private_operations}

<div class="paragraph">

Through the `LightstreamerClient` instance, you gain instant access to
all the power and complexity of Lightstreamer’s world. But, as "with
great power comes great responsibility", you must take care while using
this object: in fact, you might be unaware of triggering some action
which could mislead the normal functioning of the overlying MQTT.Cool
library.

</div>

<div class="paragraph">

The following operations are considered *private* from the MQTT.Cool
perspective, because they could negatively impact normal operation if
not properly managed. Therefore, **DO NOT USE** them in any
circumstance:

</div>

<div class="ulist">

-   [LightstreamerClient.connect](http://www.lightstreamer.com/api/ls-web-client/7.0.4/LightstreamerClient.html#connect)

-   [LightstreamerClient.disconnect](http://www.lightstreamer.com/api/ls-web-client/7.0.4/LightstreamerClient.html#disconnect)

-   [LightstreamerClient.enableSharing](http://www.lightstreamer.com/api/ls-web-client/7.0.4/LightstreamerClient.html#enableSharing)

-   [LightstreamerClient.subscribe](http://www.lightstreamer.com/api/ls-web-client/7.0.4/LightstreamerClient.html#subscribe)

-   [LightstreamerClient.unsubcribe](http://www.lightstreamer.com/api/ls-web-client/7.0.4/LightstreamerClient.html#unsubcribe)

-   [LightstreamerClient.sendMessage](http://www.lightstreamer.com/api/ls-web-client/7.0.4/LightstreamerClient.html#sendMessage)

-   any use of
    [LightstreamerClient.connectionDetails](http://www.lightstreamer.com/api/ls-web-client/7.0.4/LightstreamerClient.html#connectionDetails)

</div>

</div>

</div>

</div>

</div>

<div id="footer">

<div id="footer-text">

Version 1.1\
Last updated 2017-10-16 13:20:47 W. Europe Summer Time

</div>

</div>
