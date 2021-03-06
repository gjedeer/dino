find_packages(ENGINE_PACKAGES REQUIRED
    GDKPixbuf2
    Gee
    GIO
    GLib
    GObject
)

vala_precompile(ENGINE_VALA_C
SOURCES
    "src/core/namespace_state.vala"
    "src/core/stanza_attribute.vala"
    "src/core/stanza_node.vala"
    "src/core/stanza_reader.vala"
    "src/core/stanza_writer.vala"
    "src/core/xmpp_stream.vala"

    "src/module/bind.vala"
    "src/module/iq/module.vala"
    "src/module/iq/stanza.vala"
    "src/module/message/module.vala"
    "src/module/message/stanza.vala"
    "src/module/presence/flag.vala"
    "src/module/presence/module.vala"
    "src/module/presence/stanza.vala"
    "src/module/roster/flag.vala"
    "src/module/roster/item.vala"
    "src/module/roster/module.vala"
    "src/module/sasl.vala"
    "src/module/stanza.vala"
    "src/module/stanza_error.vala"
    "src/module/stream_error.vala"
    "src/module/tls.vala"
    "src/module/util.vala"

    "src/module/xep/0030_service_discovery/flag.vala"
    "src/module/xep/0030_service_discovery/info_result.vala"
    "src/module/xep/0030_service_discovery/items_result.vala"
    "src/module/xep/0030_service_discovery/module.vala"
    "src/module/xep/0045_muc/flag.vala"
    "src/module/xep/0045_muc/module.vala"
    "src/module/xep/0048_bookmarks/module.vala"
    "src/module/xep/0048_bookmarks/conference.vala"
    "src/module/xep/0049_private_xml_storage.vala"
    "src/module/xep/0054_vcard/module.vala"
    "src/module/xep/0060_pubsub.vala"
    "src/module/xep/0082_date_time_profiles.vala"
    "src/module/xep/0084_user_avatars.vala"
    "src/module/xep/0085_chat_state_notifications.vala"
    "src/module/xep/0115_entitiy_capabilities.vala"
    "src/module/xep/0199_ping.vala"
    "src/module/xep/0184_message_delivery_receipts.vala"
    "src/module/xep/0203_delayed_delivery.vala"
    "src/module/xep/0280_message_carbons.vala"
    "src/module/xep/0333_chat_markers.vala"
    "src/module/xep/pixbuf_storage.vala"
PACKAGES
    ${ENGINE_PACKAGES}
GENERATE_VAPI
    xmpp-vala
GENERATE_HEADER
    xmpp-vala
)

add_definitions(${VALA_CFLAGS})
add_library(xmpp-vala SHARED ${ENGINE_VALA_C})
target_link_libraries(xmpp-vala ${ENGINE_PACKAGES})

add_custom_target(xmpp-vala-vapi
DEPENDS
    ${CMAKE_BINARY_DIR}/exports/xmpp-vala.vapi
    ${CMAKE_BINARY_DIR}/exports/xmpp-vala.deps
)

install(TARGETS xmpp-vala ${TARGET_INSTALL})
install(FILES ${CMAKE_BINARY_DIR}/exports/xmpp-vala.vapi ${CMAKE_BINARY_DIR}/exports/xmpp-vala.deps DESTINATION ${VAPI_INSTALL_DIR})
install(FILES ${CMAKE_BINARY_DIR}/exports/xmpp-vala.h DESTINATION ${INCLUDE_INSTALL_DIR})