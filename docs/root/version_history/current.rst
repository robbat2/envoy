1.22.0 (pending)
================

Incompatible Behavior Changes
-----------------------------
*Changes that are expected to cause an incompatibility if applicable; deployment changes are likely required*

* tls: set TLS v1.2 as the default minimal version for servers. Users can still explicitly opt-in to 1.0 and 1.1 using :ref:`tls_minimum_protocol_version <envoy_v3_api_field_extensions.transport_sockets.tls.v3.TlsParameters.tls_minimum_protocol_version>`.

Minor Behavior Changes
----------------------
*Changes that may cause incompatibilities for some users, but should not for most*

* grpc: flip runtime guard ``envoy.reloadable_features.enable_grpc_async_client_cache`` to be default enabled. async grpc client created through getOrCreateRawAsyncClient will be cached by default.
* http: now the max concurrent streams of http2 connection can not only be adjusted down according to the SETTINGS frame but also can be adjusted up, of course, it can not exceed the configured upper bounds. This fix is guarded by ``envoy.reloadable_features.http2_allow_capacity_increase_by_settings``.

Bug Fixes
---------
*Changes expected to improve the state of the world and are unlikely to have negative effects*

* data plane: fixing error handling where writing to a socket failed while under the stack of processing. This should genreally affect HTTP/3. This behavioral change can be reverted by setting ``envoy.reloadable_features.allow_upstream_inline_write`` to false.

Removed Config or Runtime
-------------------------
*Normally occurs at the end of the* :ref:`deprecation period <deprecated>`

* http: removed ``envoy.reloadable_features.hash_multiple_header_values`` and legacy code paths.
* http: removed ``envoy.reloadable_features.require_strict_1xx_and_204_response_headers`` and ``envoy.reloadable_features.send_strict_1xx_and_204_response_headers`` and legacy code paths.
* http: removed ``envoy.reloadable_features.strip_port_from_connect`` and legacy code paths.
* http: removed ``envoy.reloadable_features.use_observable_cluster_name`` and legacy code paths.


New Features
------------
* http3: downstream HTTP/3 support is now GA! Upstream HTTP/3 also GA for specific deployments. See :ref:`here <arch_overview_http3>` for details.


Deprecated
----------

* http: removing support for long-deprecated old style filter names, e.g. envoy.router, envoy.lua.
