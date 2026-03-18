cmake_minimum_required( VERSION 3.22 )

project( SDIO_RP2350
	LANGUAGES CXX
	HOMEPAGE_URL "https://github.com/rabbitholecomputing/SDIO_RP2350"
)

set( SDIO_RP2350_DIR ${CMAKE_CURRENT_LIST_DIR} )
set( SDIO_RP2350_SOURCES
	# Sources
	"${SDIO_RP2350_DIR}/src/sdfat_sdcard_rp2350.cpp"
	"${SDIO_RP2350_DIR}/src/sdio_rp2350.cpp"
	# Private headers
	"${SDIO_RP2350_DIR}/src/sdio_rp2350.pio.h"
	# Public headers
	"${SDIO_RP2350_DIR}/include/sdio_rp2350.h"
)

add_library( SDIO_RP2350 STATIC ${SDIO_RP2350_SOURCES} )
target_include_directories( SDIO_RP2350
	PUBLIC include
	PRIVATE src
)
target_link_libraries( SDIO_RP2350
	PUBLIC
		# defined by library user, must contain root-level header `sdio_rp2350_config.h`
		SDIO_RP2350_config
	PRIVATE
		pico_stdlib
		hardware_pio
		hardware_dma
)
