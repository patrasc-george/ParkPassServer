project(HttpServer)

file(GLOB HEADER_FILES "*.h")
file(GLOB SOURCE_FILES "*.cpp")

set(CMAKE_PREFIX_PATH "/vcpkg/installed/x64-linux/share/poco" ${CMAKE_PREFIX_PATH})

add_library(${PROJECT_NAME} STATIC ${HEADER_FILES} ${SOURCE_FILES})

add_dependencies(${PROJECT_NAME} SubscriptionManager)

find_package(Poco REQUIRED COMPONENTS Foundation Net NetSSL Crypto)

target_include_directories(${PROJECT_NAME} PUBLIC 
	"${CMAKE_SOURCE_DIR}/src/SubscriptionManager"
	"${CMAKE_SOURCE_DIR}/src/QRCodeDetection"
	"${CMAKE_SOURCE_DIR}/src/WebSocketServer"
)

target_link_libraries(${PROJECT_NAME} 
	SubscriptionManager 
	QRCodeDetection
	WebSocketServer
	Poco::Net 
	Poco::NetSSL 
	Poco::Crypto
)
