cmake_minimum_required(VERSION 3.10)
project(STK)
set(CMAKE_CXX_STANDARD 14)



SET(stk_src
        ${CMAKE_CURRENT_SOURCE_DIR}/src/ADSR.cpp
        ${CMAKE_CURRENT_SOURCE_DIR}/src/Asymp.cpp
        ${CMAKE_CURRENT_SOURCE_DIR}/src/BandedWG.cpp
        ${CMAKE_CURRENT_SOURCE_DIR}/src/BeeThree.cpp
        ${CMAKE_CURRENT_SOURCE_DIR}/src/BiQuad.cpp
        ${CMAKE_CURRENT_SOURCE_DIR}/src/Blit.cpp
        ${CMAKE_CURRENT_SOURCE_DIR}/src/BlitSaw.cpp
        ${CMAKE_CURRENT_SOURCE_DIR}/src/BlitSquare.cpp
        ${CMAKE_CURRENT_SOURCE_DIR}/src/BlowBotl.cpp
        ${CMAKE_CURRENT_SOURCE_DIR}/src/BlowHole.cpp
        ${CMAKE_CURRENT_SOURCE_DIR}/src/Bowed.cpp
        ${CMAKE_CURRENT_SOURCE_DIR}/src/Brass.cpp
        ${CMAKE_CURRENT_SOURCE_DIR}/src/Chorus.cpp
        ${CMAKE_CURRENT_SOURCE_DIR}/src/Clarinet.cpp
        ${CMAKE_CURRENT_SOURCE_DIR}/src/DelayA.cpp
        ${CMAKE_CURRENT_SOURCE_DIR}/src/Delay.cpp
        ${CMAKE_CURRENT_SOURCE_DIR}/src/DelayL.cpp
        ${CMAKE_CURRENT_SOURCE_DIR}/src/Drummer.cpp
        ${CMAKE_CURRENT_SOURCE_DIR}/src/Echo.cpp
        ${CMAKE_CURRENT_SOURCE_DIR}/src/Envelope.cpp
        ${CMAKE_CURRENT_SOURCE_DIR}/src/FileLoop.cpp
        ${CMAKE_CURRENT_SOURCE_DIR}/src/FileRead.cpp
        ${CMAKE_CURRENT_SOURCE_DIR}/src/FileWrite.cpp
        ${CMAKE_CURRENT_SOURCE_DIR}/src/FileWvIn.cpp
        ${CMAKE_CURRENT_SOURCE_DIR}/src/FileWvOut.cpp
        ${CMAKE_CURRENT_SOURCE_DIR}/src/Fir.cpp
        ${CMAKE_CURRENT_SOURCE_DIR}/src/Flute.cpp
        ${CMAKE_CURRENT_SOURCE_DIR}/src/FM.cpp
        ${CMAKE_CURRENT_SOURCE_DIR}/src/FMVoices.cpp
        ${CMAKE_CURRENT_SOURCE_DIR}/src/FormSwep.cpp
        ${CMAKE_CURRENT_SOURCE_DIR}/src/FreeVerb.cpp
        ${CMAKE_CURRENT_SOURCE_DIR}/src/Granulate.cpp
        ${CMAKE_CURRENT_SOURCE_DIR}/src/Guitar.cpp
        ${CMAKE_CURRENT_SOURCE_DIR}/src/HevyMetl.cpp
        ${CMAKE_CURRENT_SOURCE_DIR}/src/Iir.cpp
        ${CMAKE_CURRENT_SOURCE_DIR}/src/include
        #${CMAKE_CURRENT_SOURCE_DIR}/src/InetWvIn.cpp
        #${CMAKE_CURRENT_SOURCE_DIR}/src/InetWvOut.cpp
        ${CMAKE_CURRENT_SOURCE_DIR}/src/JCRev.cpp
        ${CMAKE_CURRENT_SOURCE_DIR}/src/LentPitShift.cpp
        ${CMAKE_CURRENT_SOURCE_DIR}/src/Makefile
        ${CMAKE_CURRENT_SOURCE_DIR}/src/Makefile.in
        ${CMAKE_CURRENT_SOURCE_DIR}/src/Mandolin.cpp
        ${CMAKE_CURRENT_SOURCE_DIR}/src/Mesh2D.cpp
        ${CMAKE_CURRENT_SOURCE_DIR}/src/Messager.cpp
        ${CMAKE_CURRENT_SOURCE_DIR}/src/MidiFileIn.cpp
        ${CMAKE_CURRENT_SOURCE_DIR}/src/ModalBar.cpp
        ${CMAKE_CURRENT_SOURCE_DIR}/src/Modal.cpp
        ${CMAKE_CURRENT_SOURCE_DIR}/src/Modulate.cpp
        ${CMAKE_CURRENT_SOURCE_DIR}/src/Moog.cpp
        ${CMAKE_CURRENT_SOURCE_DIR}/src/Mutex.cpp
        ${CMAKE_CURRENT_SOURCE_DIR}/src/Noise.cpp
        ${CMAKE_CURRENT_SOURCE_DIR}/src/NRev.cpp
        ${CMAKE_CURRENT_SOURCE_DIR}/src/OnePole.cpp
        ${CMAKE_CURRENT_SOURCE_DIR}/src/OneZero.cpp
        ${CMAKE_CURRENT_SOURCE_DIR}/src/PercFlut.cpp
        ${CMAKE_CURRENT_SOURCE_DIR}/src/Phonemes.cpp
        ${CMAKE_CURRENT_SOURCE_DIR}/src/PitShift.cpp
        ${CMAKE_CURRENT_SOURCE_DIR}/src/Plucked.cpp
        ${CMAKE_CURRENT_SOURCE_DIR}/src/PoleZero.cpp
        ${CMAKE_CURRENT_SOURCE_DIR}/src/PRCRev.cpp
        ${CMAKE_CURRENT_SOURCE_DIR}/src/Recorder.cpp
        ${CMAKE_CURRENT_SOURCE_DIR}/src/Resonate.cpp
        ${CMAKE_CURRENT_SOURCE_DIR}/src/Rhodey.cpp
        ${CMAKE_CURRENT_SOURCE_DIR}/src/RtAudio.cpp
        ${CMAKE_CURRENT_SOURCE_DIR}/src/RtMidi.cpp
        ${CMAKE_CURRENT_SOURCE_DIR}/src/RtWvIn.cpp
        ${CMAKE_CURRENT_SOURCE_DIR}/src/RtWvOut.cpp
        ${CMAKE_CURRENT_SOURCE_DIR}/src/Sampler.cpp
        ${CMAKE_CURRENT_SOURCE_DIR}/src/Saxofony.cpp
        ${CMAKE_CURRENT_SOURCE_DIR}/src/Shakers.cpp
        ${CMAKE_CURRENT_SOURCE_DIR}/src/Simple.cpp
        ${CMAKE_CURRENT_SOURCE_DIR}/src/SineWave.cpp
        ${CMAKE_CURRENT_SOURCE_DIR}/src/SingWave.cpp
        ${CMAKE_CURRENT_SOURCE_DIR}/src/Sitar.cpp
        ${CMAKE_CURRENT_SOURCE_DIR}/src/Skini.cpp
        ${CMAKE_CURRENT_SOURCE_DIR}/src/Socket.cpp
        ${CMAKE_CURRENT_SOURCE_DIR}/src/Sphere.cpp
        ${CMAKE_CURRENT_SOURCE_DIR}/src/StifKarp.cpp
        ${CMAKE_CURRENT_SOURCE_DIR}/src/Stk.cpp
        ${CMAKE_CURRENT_SOURCE_DIR}/src/TapDelay.cpp
        #${CMAKE_CURRENT_SOURCE_DIR}/src/TcpClient.cpp
        #${CMAKE_CURRENT_SOURCE_DIR}/src/TcpServer.cpp
        ${CMAKE_CURRENT_SOURCE_DIR}/src/Thread.cpp
        ${CMAKE_CURRENT_SOURCE_DIR}/src/TubeBell.cpp
        ${CMAKE_CURRENT_SOURCE_DIR}/src/Twang.cpp
        ${CMAKE_CURRENT_SOURCE_DIR}/src/TwoPole.cpp
        ${CMAKE_CURRENT_SOURCE_DIR}/src/TwoZero.cpp
        #${CMAKE_CURRENT_SOURCE_DIR}/src/UdpSocket.cpp
        ${CMAKE_CURRENT_SOURCE_DIR}/src/Voicer.cpp
        ${CMAKE_CURRENT_SOURCE_DIR}/src/VoicForm.cpp
        ${CMAKE_CURRENT_SOURCE_DIR}/src/Whistle.cpp
        )
include_directories(${CMAKE_CURRENT_SOURCE_DIR}/include)
add_library(stk STATIC ${stk_src})

if (UNIX)
    target_compile_definitions(stk INTERFACE -D__LINUX_ALSA__ INTERFACE -DHAVE_GETTIMEOFDAY PRIVATE -D__OS_LINUX__)
elseif(WIN32)
	target_compile_definitions(stk INTERFACE -D__WINDOWS_MM__ INTERFACE -D__WINDOWS_DS__ PRIVATE -D__OS_WINDOWS__)
endif(UNIX)
    target_compile_definitions(stk INTERFACE -D__LITTLE_ENDIAN__ INTERFACE -DRAWWAVE_PATH=\"${CMAKE_CURRENT_SOURCE_DIR}/rawwaves/\")

if(UNIX)
    target_link_libraries(stk pthread asound)
elseif(WIN32)
	target_link_libraries(stk winmm dsound)
endif(UNIX)