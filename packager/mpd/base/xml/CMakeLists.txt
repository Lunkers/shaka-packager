target_sources(mpd_builder PRIVATE
    xml_node.cc
    scoped_xml_ptr.h
)

target_sources(mpd_base_unittest PRIVATE
    xml_node_unittest.cc
)