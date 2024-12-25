cmake_minimum_required(VERSION 3.1)
project(regamedll CXX)

set(CMAKE_CXX_STANDARD 14)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

if(ANDROID)
	set(REGAME_LIB server)
elseif(WIN32)
	set(REGAME_LIB mp)
else()
	set(REGAME_LIB cs)
endif()

set(PROJECT_SRC_DIR
	"${PROJECT_SOURCE_DIR}"
	"${PROJECT_SOURCE_DIR}/engine"
	"${PROJECT_SOURCE_DIR}/common"
	"${PROJECT_SOURCE_DIR}/dlls"
	"${PROJECT_SOURCE_DIR}/game_shared"
	"${PROJECT_SOURCE_DIR}/pm_shared"
	"${PROJECT_SOURCE_DIR}/regamedll"
	"${PROJECT_SOURCE_DIR}/unittests"
)

set(PROJECT_PUBLIC_DIR
	"${PROJECT_SOURCE_DIR}/public"
	"${PROJECT_SOURCE_DIR}/public/regamedll"
)

set(ENGINE_SRCS
	"engine/unicode_strtools.cpp"
)

set(SHARED_SRCS
	"game_shared/shared_util.cpp"
	"game_shared/voice_gamemgr.cpp"
	"game_shared/bot/bot.cpp"
	"game_shared/bot/bot_manager.cpp"
	"game_shared/bot/bot_profile.cpp"
	"game_shared/bot/bot_util.cpp"
	"game_shared/bot/nav_area.cpp"
	"game_shared/bot/nav_file.cpp"
	"game_shared/bot/nav_node.cpp"
	"game_shared/bot/nav_path.cpp"
	"pm_shared/pm_debug.cpp"
	"pm_shared/pm_math.cpp"
	"pm_shared/pm_shared.cpp"
	"regamedll/regamedll.cpp"
	"regamedll/precompiled.cpp"
	"regamedll/public_amalgamation.cpp"
	"regamedll/hookchains_impl.cpp"
	"regamedll/sse_mathfun.cpp"
	"public/FileSystem.cpp"
	"public/interface.cpp"
	"public/MemPool.cpp"
)

set(GAMEDLL_SRCS
	"dlls/airtank.cpp"
	"dlls/ammo.cpp"
	"dlls/animating.cpp"
	"dlls/animation.cpp"
	"dlls/basemonster.cpp"
	"dlls/bmodels.cpp"
	"dlls/buttons.cpp"
	"dlls/career_tasks.cpp"
	"dlls/cbase.cpp"
	"dlls/client.cpp"
	"dlls/cmdhandler.cpp"
	"dlls/combat.cpp"
	"dlls/debug.cpp"
	"dlls/doors.cpp"
	"dlls/effects.cpp"
	"dlls/explode.cpp"
	"dlls/func_break.cpp"
	"dlls/func_tank.cpp"
	"dlls/game.cpp"
	"dlls/gamerules.cpp"
	"dlls/ggrenade.cpp"
	"dlls/gib.cpp"
	"dlls/globals.cpp"
	"dlls/h_battery.cpp"
	"dlls/h_cycler.cpp"
	"dlls/h_export.cpp"
	"dlls/healthkit.cpp"
	"dlls/hintmessage.cpp"
	"dlls/items.cpp"
	"dlls/lights.cpp"
	"dlls/mapinfo.cpp"
	"dlls/maprules.cpp"
	"dlls/mortar.cpp"
	"dlls/multiplay_gamerules.cpp"
	"dlls/observer.cpp"
	"dlls/pathcorner.cpp"
	"dlls/plats.cpp"
	"dlls/player.cpp"
	"dlls/revert_saved.cpp"
	"dlls/saverestore.cpp"
	"dlls/singleplay_gamerules.cpp"
	"dlls/skill.cpp"
	"dlls/sound.cpp"
	"dlls/soundent.cpp"
	"dlls/spectator.cpp"
	"dlls/subs.cpp"
	"dlls/training_gamerules.cpp"
	"dlls/triggers.cpp"
	"dlls/tutor.cpp"
	"dlls/tutor_base_states.cpp"
	"dlls/tutor_base_tutor.cpp"
	"dlls/tutor_cs_states.cpp"
	"dlls/tutor_cs_tutor.cpp"
	"dlls/util.cpp"
	"dlls/vehicle.cpp"
	"dlls/weapons.cpp"
	"dlls/weapontype.cpp"
	"dlls/world.cpp"
	"dlls/API/CAPI_Impl.cpp"
	"dlls/API/CSEntity.cpp"
	"dlls/API/CSPlayer.cpp"
	"dlls/API/CSPlayerItem.cpp"
	"dlls/API/CSPlayerWeapon.cpp"
	"dlls/addons/item_airbox.cpp"
	"dlls/addons/point_command.cpp"
	"dlls/addons/trigger_random.cpp"
	"dlls/addons/trigger_setorigin.cpp"
	"dlls/wpn_shared/wpn_ak47.cpp"
	"dlls/wpn_shared/wpn_aug.cpp"
	"dlls/wpn_shared/wpn_awp.cpp"
	"dlls/wpn_shared/wpn_c4.cpp"
	"dlls/wpn_shared/wpn_deagle.cpp"
	"dlls/wpn_shared/wpn_elite.cpp"
	"dlls/wpn_shared/wpn_famas.cpp"
	"dlls/wpn_shared/wpn_fiveseven.cpp"
	"dlls/wpn_shared/wpn_flashbang.cpp"
	"dlls/wpn_shared/wpn_g3sg1.cpp"
	"dlls/wpn_shared/wpn_galil.cpp"
	"dlls/wpn_shared/wpn_glock18.cpp"
	"dlls/wpn_shared/wpn_hegrenade.cpp"
	"dlls/wpn_shared/wpn_knife.cpp"
	"dlls/wpn_shared/wpn_m3.cpp"
	"dlls/wpn_shared/wpn_m4a1.cpp"
	"dlls/wpn_shared/wpn_m249.cpp"
	"dlls/wpn_shared/wpn_mac10.cpp"
	"dlls/wpn_shared/wpn_mp5navy.cpp"
	"dlls/wpn_shared/wpn_p90.cpp"
	"dlls/wpn_shared/wpn_p228.cpp"
	"dlls/wpn_shared/wpn_scout.cpp"
	"dlls/wpn_shared/wpn_sg550.cpp"
	"dlls/wpn_shared/wpn_sg552.cpp"
	"dlls/wpn_shared/wpn_smokegrenade.cpp"
	"dlls/wpn_shared/wpn_tmp.cpp"
	"dlls/wpn_shared/wpn_ump45.cpp"
	"dlls/wpn_shared/wpn_usp.cpp"
	"dlls/wpn_shared/wpn_xm1014.cpp"
	"dlls/bot/cs_bot.cpp"
	"dlls/bot/cs_bot_chatter.cpp"
	"dlls/bot/cs_bot_event.cpp"
	"dlls/bot/cs_bot_init.cpp"
	"dlls/bot/cs_bot_learn.cpp"
	"dlls/bot/cs_bot_listen.cpp"
	"dlls/bot/cs_bot_manager.cpp"
	"dlls/bot/cs_bot_nav.cpp"
	"dlls/bot/cs_bot_pathfind.cpp"
	"dlls/bot/cs_bot_radio.cpp"
	"dlls/bot/cs_bot_statemachine.cpp"
	"dlls/bot/cs_bot_update.cpp"
	"dlls/bot/cs_bot_vision.cpp"
	"dlls/bot/cs_bot_weapon.cpp"
	"dlls/bot/cs_gamestate.cpp"
	"dlls/bot/states/cs_bot_attack.cpp"
	"dlls/bot/states/cs_bot_buy.cpp"
	"dlls/bot/states/cs_bot_defuse_bomb.cpp"
	"dlls/bot/states/cs_bot_escape_from_bomb.cpp"
	"dlls/bot/states/cs_bot_fetch_bomb.cpp"
	"dlls/bot/states/cs_bot_follow.cpp"
	"dlls/bot/states/cs_bot_hide.cpp"
	"dlls/bot/states/cs_bot_hunt.cpp"
	"dlls/bot/states/cs_bot_idle.cpp"
	"dlls/bot/states/cs_bot_investigate_noise.cpp"
	"dlls/bot/states/cs_bot_move_to.cpp"
	"dlls/bot/states/cs_bot_plant_bomb.cpp"
	"dlls/bot/states/cs_bot_use_entity.cpp"
	"dlls/hostage/hostage.cpp"
	"dlls/hostage/hostage_improv.cpp"
	"dlls/hostage/hostage_localnav.cpp"
	"dlls/hostage/states/hostage_animate.cpp"
	"dlls/hostage/states/hostage_escape.cpp"
	"dlls/hostage/states/hostage_follow.cpp"
	"dlls/hostage/states/hostage_idle.cpp"
	"dlls/hostage/states/hostage_retreat.cpp"
)

if(MSVC)
	set(GAMEDLL_SRCS ${GAMEDLL_SRCS} "msvc/mp.def" "public/tier0/dbg.cpp")
endif()

add_library(${REGAME_LIB} MODULE ${appversion.sh})

if (NOT TARGET appversion)
	add_custom_target(appversion DEPENDS COMMAND "${PROJECT_SOURCE_DIR}/version/appversion.sh" "${PROJECT_SOURCE_DIR}/..")
endif()

add_dependencies(${REGAME_LIB} appversion)

target_include_directories(${REGAME_LIB} PRIVATE
	${PROJECT_SRC_DIR}
	${PROJECT_CPPUNITLITE_DIR}
	${PROJECT_PUBLIC_DIR}
)

target_compile_definitions(${REGAME_LIB} PRIVATE
	REGAMEDLL_FIXES
	REGAMEDLL_API
	REGAMEDLL_ADD
	UNICODE_FIXES
	BUILD_LATEST
	CLIENT_WEAPONS
	USE_QSTRING
	NDEBUG
)

if(NOT MSVC)
	target_compile_definitions(${REGAME_LIB} PRIVATE
		_LINUX
		LINUX
		_GLIBCXX_USE_CXX11_ABI=0
		_stricmp=strcasecmp
		_strnicmp=strncasecmp
		_strdup=strdup
		_unlink=unlink
		_vsnprintf=vsnprintf
		_write=write
		_close=close
		_access=access
		_vsnwprintf=vswprintf
	)

    target_compile_options(${REGAME_LIB} PRIVATE
        -U_FORTIFY_SOURCE
        -fms-extensions
        -fpermissive
        -Wno-write-strings
        -fno-exceptions
    )
endif()

target_sources(${REGAME_LIB} PRIVATE
	${GAMEDLL_SRCS}
	${ENGINE_SRCS}
	${SHARED_SRCS}
)

set_target_postfix(${REGAME_LIB})

if(MSVC)
	add_definitions(-D_CRT_SECURE_NO_WARNINGS -D_CRT_NONSTDC_NO_DEPRECATE)

	# Install PDB file on Windows
	install(FILES $<TARGET_PDB_FILE:${REGAME_LIB}>
		DESTINATION "${GAME_DIR}/${SERVER_INSTALL_DIR}/" OPTIONAL)
else()
	target_link_libraries(${REGAME_LIB} PRIVATE dl)

	# if(CMAKE_SIZEOF_VOID_P EQUAL 4)
	# 	set(LINK_FLAGS "${LINK_FLAGS} -L${PROJECT_SOURCE_DIR}/lib/linux32")
	# 	target_link_libraries(regamedll PRIVATE aelf32)
	# 	set_target_properties(regamedll PROPERTIES POSITION_INDEPENDENT_CODE OFF)
	# endif()

	set(LINK_FLAGS "${LINK_FLAGS} -Wl,-rpath,'$ORIGIN/.'")
endif()

install(TARGETS ${REGAME_LIB}
		DESTINATION "${GAME_DIR}/${SERVER_INSTALL_DIR}/"
		PERMISSIONS OWNER_READ OWNER_WRITE OWNER_EXECUTE
		GROUP_READ GROUP_EXECUTE
		WORLD_READ WORLD_EXECUTE)
