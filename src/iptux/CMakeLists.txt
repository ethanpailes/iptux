pkg_check_modules (IPTUX REQUIRED glib-2.0>=2.32.0 gthread-2.0>=2.14.0 gtk+-3.0 jsoncpp>=1.0)
include_directories("${PROJECT_SOURCE_DIR}/src" "${PROJECT_BINARY_DIR}/src" "${IPTUX_INCLUDE_DIRS}")
link_libraries("${IPTUX_LIBRARIES}")
link_libraries("${Intl_LIBRARIES}")
if(GST_FOUND)
	include_directories("${GST_INCLUDE_DIRS}")
	link_libraries("${GST_LIBRARIES}")
endif(GST_FOUND)

add_library(iptux
	STATIC
	AnalogFS.cpp
	Application.cpp
	callback.cpp
	Command.cpp
	CoreThread.cpp
	DataSettings.cpp
	DetectPal.cpp
	dialog.cpp
	DialogBase.cpp
	DialogGroup.cpp
	DialogPeer.cpp
    global.cpp
	HelpDialog.cpp
	IptuxConfig.cpp
	LogSystem.cpp
	MainWindow.cpp
	mess.cpp
	output.cpp
	ProgramData.cpp
	RecvFile.cpp
	RecvFileData.cpp
	RevisePal.cpp
	SendFile.cpp
	SendFileData.cpp
	ShareFile.cpp
	SoundSystem.cpp
	StatusIcon.cpp
	support.cpp
	TcpData.cpp
	UdpData.cpp
	utils.cpp
	wrapper.cpp
	WindowConfig.cpp
        TransWindow.cpp TransWindow.h TransFileModel.cpp TransFileModel.h TransAbstract.cpp TransAbstract.h UiUtils.cpp UiUtils.h)


add_executable(libiptux_test
    IptuxConfigTest.cpp
	UtilsTest.cpp
	TestMain.cpp
	)
if(GTEST_FOUND)
	include_directories(${GTEST_INCLUDE_DIRS})
	target_link_libraries(libiptux_test ${GTEST_BOTH_LIBRARIES} iptux pthread)
else()
	target_link_libraries(libiptux_test gtest iptux)
endif()
add_test(NAME libiptux_test COMMAND libiptux_test)
