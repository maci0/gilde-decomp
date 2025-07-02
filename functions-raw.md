zlib_adler32	10001000	uLong zlib_adler32(uLong adler, Bytef * buf, uInt len)	302
srv_SendBroadcast	10001130	void srv_SendBroadcast(ushort port, char * b_message)	179
zlib_crc32	100011f0	ulong zlib_crc32(ulong crc, uchar * buf, uint len)	309
zlib_deflateInit2_	10001330	int zlib_deflateInit2_(void * strm, int level, int method, int windowBits, int memLevel, int strategy, char * version, int stream_size)	505
zlib_deflateReset	10001530	int zlib_deflateReset(void * strm)	115
zlib_deflate	100015b0	int zlib_deflate(void * strm, int flush)	685
zlib_write_to_buffer	10001860	void zlib_write_to_buffer(void * s, uint16_t val)	47
zlib_flush_buffer	10001890	void zlib_flush_buffer(void * strm)	114
zlib_deflateEnd	10001910	int zlib_deflateEnd(void * strm)	170
zlib_reset_data	100019c0	void zlib_reset_data(void * s)	147
zlib_deflate_stored	10001a60	int zlib_deflate_stored(void * s, int flush)	343
zlib_fill_window	10001bc0	void zlib_fill_window(void * s)	290
zlib_read_buf	10001cf0	uint32_t zlib_read_buf(void * strm, byte * buf, uint32_t len)	113
zlib_deflate_slow	10001d71	uint zlib_deflate_slow(undefined4 param_1, int * param_2, int param_3)	812
zlib_boyer_moore_search	100020a0	char * zlib_boyer_moore_search(int param_1, uint param_2)	367
zlib_deflate_fast	10002210	uint zlib_deflate_fast(int * param_1, int param_2)	1066
logEvent	10002640	void logEvent(LPCSTR message, byte flags, int log_level)	290
unhandledExceptionHandler	10002770	long unhandledExceptionHandler(_EXCEPTION_POINTERS * ExceptionInfo)	1836
writeArchiveFile	10002fc0	uint32_t writeArchiveFile(void * archive_info)	376
getDataBlock	10003140	int * getDataBlock(int data_structure, uint block_index)	33
checkMemoryProtection	10003170	int checkMemoryProtection(uint32_t address)	95
analyzeBytePattern	10003260	uint32_t analyzeBytePattern(int pattern, int length, int baseAddress, int * outStartAddress)	183
errorHandlerInit	10003320	void errorHandlerInit(void * exception_callback, void * user_data, HWND main_window_handle, uint32_t init_flags)	404
errorHandlerCleanup	100034c0	void errorHandlerCleanup(void)	83
fatal_error	10003520	void fatal_error(LPCSTR file_name, uint32_t line_number, LPCSTR error_message)	160
showMessage	100035c0	void showMessage(LPCSTR message_text)	119
logMessage	10003640	void logMessage(LPCSTR file, int line, LPCSTR message, int log_type)	132
zlib_parseGzipHeader	100036d0	void zlib_parseGzipHeader(void * strm)	332
zlib_getByte	10003820	uint32_t zlib_getByte(void * strm)	114
zlib_gzclose	100038a0	int zlib_gzclose(void * file)	177
zlib_readFromStream	10003960	int zlib_readFromStream(void * strm, byte * buffer, int length)	559
zlib_writeToStream	10003b90	uint32_t zlib_writeToStream(void * strm, int flush)	182
zlib_getLong	10003c50	uint32_t zlib_getLong(void * strm)	65
zlib_destroy	10003ca0	int zlib_destroy(void * s)	77
zlib_putLong	10003cf0	void zlib_putLong(void * file_handle, uint32_t value)	43
zlib_inflateReset	10003d20	int zlib_inflateReset(void * strm)	123
zlib_inflateInit2_	10003da0	int zlib_inflateInit2_(void * z, int w, char * version, int stream_size)	160
zlib_inflate	10003e40	int zlib_inflate(void * z, int f)	3263
zlib_inflateEnd	10004b40	int zlib_inflateEnd(void * z)	57
zlib_tr_init	10004b80	void zlib_tr_init(void * s, uint8_t param_2, uint32_t param_3, uint32_t param_4, void * strm)	57
zlib_inflate_codes	10004bc0	int zlib_inflate_codes(void * s, void * strm, int flush)	1919
zlib_inflate_trees_free	10005370	void zlib_inflate_trees_free(void * table, void * strm)	20
zlib_inflate_fast	10005390	int zlib_inflate_fast(uint32_t lit_len_table_idx, uint32_t dist_table_idx, void * lit_len_table_ptr, void * dist_table_ptr, void * s, void * strm)	911
zlib_inflate_blocks_reset	10005720	int zlib_inflate_blocks_reset(void * strm)	66
zlib_inflate_blocks_free	10005770	int zlib_inflate_blocks_free(void * strm)	72
zlib_inflate_blocks_new	100057c0	int zlib_inflate_blocks_new(void * strm, int window_bits, char * version, int stream_size)	270
zlib_inflate_blocks	100058d0	int zlib_inflate_blocks(void * strm, int flush)	1015
zlib_inflate_trees_dynamic	10005d00	int zlib_inflate_trees_dynamic(void * s, void * * lit_len_table, void * * dist_table, void * * code_len_table, void * strm)	163
zlib_huft_build	10005db0	int zlib_huft_build(int * lengths, uint32_t num_codes, uint32_t max_codes, void * base_table, void * extra_bits_table, uint32_t * table_ptr, uint32_t * max_length_ptr, void * work_space, uint32_t * table_size_ptr, uint32_t * codes)	1225
zlib_inflate_trees_bits	10006280	int zlib_inflate_trees_bits(uint32_t num_lit_len_codes, uint32_t num_dist_codes, int * code_lengths, uint32_t * max_lit_len_bits, uint32_t * max_dist_bits, uint32_t * lit_len_table, uint32_t * dist_table, void * work_space, void * strm)	393
zlib_inflate_trees_fixed	10006410	int zlib_inflate_trees_fixed(uint32_t * lit_len_table_ptr, uint32_t * dist_table_ptr, uint32_t * lit_len_codes_ptr, uint32_t * dist_codes_ptr)	46
zlib_inflate_flush	10006440	int zlib_inflate_flush(void * s, void * strm, int status)	306
m_alloc_debug	10006580	void * m_alloc_debug(size_t size, char * tag)	658
m_free	10006820	void m_free(void * ptr)	188
m_alloc_init	100068e0	void m_alloc_init(int max_allocations)	162
m_alloc_dump	10006990	void m_alloc_dump(char * filter_tag)	612
m_alloc_cleanup	10006c00	void m_alloc_cleanup(void)	283
m_pool_alloc	10006d20	int * m_pool_alloc(int * pool_handle, uint size, int count)	270
m_pool_free	10006e30	void m_pool_free(void * * pool_handle, void * ptr)	137
zlib_ct_init	10006ec0	void zlib_ct_init(void * s)	108
noop	10006f30	void noop(void)	1
zlib_tr_tally	10006f40	void zlib_tr_tally(void * s)	102
zlib_tr_flush_block	10006fb0	void zlib_tr_flush_block(void * s, uint32_t param_2, uint32_t param_3, int param_4)	157
zlib_ct_tally	10007050	void zlib_ct_tally(void * s)	597
zlib_trees_bi_flush	100072b0	void zlib_trees_bi_flush(void * s)	494
zlib_build_tree	100074a0	void zlib_build_tree(void * s, void * desc)	563
zlib_pqdownheap	100076e0	void zlib_pqdownheap(void * s, void * tree, int k)	209
zlib_gen_codes	100077c0	void zlib_gen_codes(void * s, void * tree_desc)	545
zlib_gen_bitlen	100079f0	void zlib_gen_bitlen(void * tree, int max_code, void * bl_count)	115
zlib_zlib_build_static_trees	10007a70	void zlib_zlib_build_static_trees(void * s)	111
zlib_scan_tree	10007ae0	void zlib_scan_tree(void * s, void * tree, int max_code)	231
zlib_send_tree	10007bd0	void zlib_send_tree(void * s, int num_lit_len_codes, int num_dist_codes, int num_code_len_codes)	613
zlib_send_codes	10007e40	void zlib_send_codes(void * s, void * tree, uint16_t max_code)	1397
zlib_send_all_trees	100083c0	void zlib_send_all_trees(void * s, void * lit_len_tree, void * dist_tree)	1083
zlib_build_bl_tree	10008800	int zlib_build_bl_tree(void * s)	116
zlib_bi_reverse	10008880	uint zlib_bi_reverse(uint code, int len)	31
zlib_bi_windup	100088a0	void zlib_bi_windup(void * s)	139
zlib_tr_align	10008930	void zlib_tr_align(void * s)	124
zlib_tr_stored_block	100089b0	void zlib_tr_stored_block(void * s, uint8_t * buf, uint32_t len, int last_block)	151
CRT_fclose	10008a50	int CRT_fclose(FILE * stream)	53
CRT_fread	10008a90	size_t CRT_fread(void * buffer, size_t size, size_t count, FILE * stream)	492
vfs_close_and_free	10008c80	int vfs_close_and_free(void * file_ptr)	129
vfs_read_data	10008d10	uint32_t vfs_read_data(void * file_data)	301
vfs_read	10008e40	uint32_t vfs_read(void * output_buffer, int element_size, int element_count, void * vfs_file_data)	472
vfs_open	10009020	int * vfs_open(byte * file_data, uint file_data_len, char * open_mode)	667
zlib_zcalloc	100092e0	undefined zlib_zcalloc(undefined4 opaque, int items, int size)	19
mem_FreeWrapper	10009300	undefined mem_FreeWrapper(undefined4 param_1, void * param_2)	12
CRT_DllMain_stub	10009310	int CRT_DllMain_stub(void)	8
Init	10009320	BOOL Init(LPVOID p_ServerInitParams)	42
Exit	10009350	void Exit(void)	68
srv_GameLoop	100093a0	uint32_t srv_GameLoop(void * server_params)	2434
srv_InitServer	10009d30	void srv_InitServer(void)	296
srv_InitSockets	10009e60	int srv_InitSockets(void)	419
srv_Cleanup	1000a010	void srv_Cleanup(void)	112
srv_AcceptClient	1000a080	uint32_t srv_AcceptClient(void)	600
srv_CloseClientConnection	1000a2e0	int srv_CloseClientConnection(void * client_slot)	96
srv_RecvFromClient	1000a340	int srv_RecvFromClient(void * client_slot)	336
srv_SendData	1000a490	int srv_SendData(void * client_slot)	211
srv_ProcessClientCommands	1000a570	int srv_ProcessClientCommands(void)	750
srv_SendQueuedCommands	1000a860	int srv_SendQueuedCommands(void)	131
enqueue_client_command	1000a8f0	int enqueue_client_command(void * client_slot, void * command_data)	170
enqueue_client_command_alt	1000a9a0	int enqueue_client_command_alt(void * client, void * command_data)	170
dequeue_command	1000aa50	void dequeue_command(void * client_data, void * command)	97
srv_DispatchGameCommand	1000aac0	int srv_DispatchGameCommand(void)	639
srv_HandleWinsockError	1000ad40	void srv_HandleWinsockError(uint32_t error_code)	600
amt_init	1000b040	void amt_init(void)	372
amt_validate	1000b1c0	int amt_validate(void * office_application_data)	205
amt_assign_player	1000b290	int amt_assign_player(void * office_assignment_data)	425
amt_validate_action	1000b440	int amt_validate_action(void * office_action_data)	133
amt_perform_action	1000b4d0	int amt_perform_action(void * office_action_data)	836
amt_register_player	1000b820	void amt_register_player(uint32_t player_id)	42
amt_unregister_player	1000b850	void amt_unregister_player(uint32_t player_id)	42
amt_swap_players	1000b880	int amt_swap_players(void * office_swap_data)	263
amt_remove_player	1000b990	int amt_remove_player(void * player_info)	157
amt_remove_player_with_cleanup	1000ba30	void amt_remove_player_with_cleanup(void * player_info, int cleanup_flags)	179
amt_fio_LoadAemter	1000baf0	int amt_fio_LoadAemter(void * file_handle, uint32_t file_size)	606
amt_player_init	1000bd50	void amt_player_init(void * player_info)	66
amt_is_player_in_amt	1000bda0	bool amt_is_player_in_amt(void * player_info)	70
ahm_ExAllocAlchemist	1000bdf0	uint16_t ahm_ExAllocAlchemist(void * player_info)	1002
gm_setPlayerAttributes	1000c1e0	int gm_setPlayerAttributes(void * attribute_data, int attribute_value)	130
gm_addPlayerToBuilding	1000c280	int gm_addPlayerToBuilding(void * player_info, void * building_info, void * game_info)	130
gm_removePlayerFromBuilding	1000c310	int gm_removePlayerFromBuilding(void * player_info, void * building_info, void * game_info)	110
gm_updatePlayerBuilding	1000c380	int gm_updatePlayerBuilding(void * player_info, void * building_info)	51
gm_updatePlayerDesire	1000c3c0	int gm_updatePlayerDesire(void * player_info, void * desire_info)	83
inv_clear_slot	1000c420	int inv_clear_slot(uint32_t player_id, void * player_inventory, void * game_info)	166
alm_load_data	1000c4d0	int alm_load_data(void * file_handle, void * alchemist_data)	295
gm_allocAlchemist	1000c600	char * gm_allocAlchemist(void)	109
alm_get_by_id	1000c670	undefined4 * alm_get_by_id(int alchemist_id)	45
alm_process_turn	1000c6a0	void alm_process_turn(void * game_data)	102
cm_get_size	1000c710	int cm_get_size(void * command)	340
cm_process	1000ca00	int cm_process(void * command)	130
gm_getPlayerConnection	1000ca90	int gm_getPlayerConnection(void * player_info, int connection_type)	130
cm_ChkMoveCredits	1000cb20	undefined4 cm_ChkMoveCredits(void * param_1)	171
cm_ChkSellObjekt	1000cbd0	undefined4 cm_ChkSellObjekt(short * command_data)	517
cm_ChkChangeAttribute	1000cde0	undefined4 cm_ChkChangeAttribute(void * param_1)	331
cm_ChkChangeBits	1000cf30	undefined4 cm_ChkChangeBits(void * command_data)	162
cm_ChkSetGebBesitzer	1000cfe0	undefined4 cm_ChkSetGebBesitzer(void)	64
amt_is_valid	1000d020	bool amt_is_valid(int command_data)	22
amt_is_action_valid	1000d040	bool amt_is_action_valid(int command_data)	22
cm_CanBuyItem	1000d060	bool cm_CanBuyItem(void * command_data)	169
cm_ValidateLobbyAction	1000d110	bool cm_ValidateLobbyAction(void * command_data)	333
cm_ChkCutsceneReady	1000d260	int cm_ChkCutsceneReady(void * command_data)	120
cm_handle_invalid	1000d2e0	undefined4 cm_handle_invalid(char * command_data, undefined1 * result_ptr)	77
cm_Stub	1000d330	undefined4 cm_Stub(undefined4 command_data, undefined1 * result_ptr)	14
cm_NotYetImplemented	1000d340	undefined4 cm_NotYetImplemented(void)	6
cm_ExAllocGebaeude	1000d350	undefined4 cm_ExAllocGebaeude(void * command_data, undefined1 * result_ptr)	267
cm_ExAllocSpieler_2	1000d460	undefined4 cm_ExAllocSpieler_2(void * command_data, undefined1 * result_ptr)	267
cm_ExAllocSpieler	1000d570	undefined4 cm_ExAllocSpieler(int command_data, undefined1 * result_ptr)	361
cm_ExChangePlayerIdentity	1000d6e0	undefined4 cm_ExChangePlayerIdentity(int command_data)	78
cm_ExFree	1000d730	undefined4 cm_ExFree(void * command_data, undefined1 * result_ptr)	180
cm_ExSellObject	1000d7f0	undefined4 cm_ExSellObject(void * command_data, undefined1 * result_ptr)	164
move_object	1000d8a0	undefined4 move_object(void * command_data, undefined1 * result_ptr)	142
cm_ExSellObjekt	1000d930	undefined4 cm_ExSellObjekt(void * command_data, undefined1 * result_ptr)	2057
cm_ExProdObjekt	1000e140	undefined4 cm_ExProdObjekt(void * command_data, undefined1 * result_ptr)	993
cm_ExMoveObjekt	1000e533	undefined4 cm_ExMoveObjekt(void * command_data, undefined4 unknown_param_2, void * param_3, undefined1 * result_ptr)	343
cm_ExClearLagerslot	1000e690	int cm_ExClearLagerslot(void * player_data, uint8_t * status_flag)	191
cm_ExAllocObject	1000e750	undefined4 cm_ExAllocObject(void * param_1, undefined1 * param_2)	123
cm_ExChangeAttribute	1000e7d0	undefined4 cm_ExChangeAttribute(void * command_data, undefined1 * result_ptr)	242
cm_ExSetAttribute	1000e8d0	undefined4 cm_ExSetAttribute(void * param_1, undefined1 * param_2)	239
cm_ExChangeDesire	1000e9c0	int cm_ExChangeDesire(void * player_data, uint8_t * status_flag)	214
cm_ExchangeBits	1000eaa0	undefined4 cm_ExchangeBits(void * param_1, undefined1 * param_2)	145
cm_ExchangeBits_Helper1	1000eb31	undefined cm_ExchangeBits_Helper1(void)	25
cm_ExchangeBits_Helper2	1000eb4a	undefined4 cm_ExchangeBits_Helper2(void)	20
cm_ExchangeBits_Success	1000eb5e	undefined4 cm_ExchangeBits_Success(void)	18
cm_ExchangeFloat	1000eb70	undefined4 cm_ExchangeFloat(void * param_1, undefined1 * param_2)	135
cm_AdjustRelationship	1000ec00	undefined4 cm_AdjustRelationship(void * param_1, undefined1 * param_2)	901
cm_SetNextAktion	1000ef90	undefined4 cm_SetNextAktion(int param_1)	26
cm_HandleClientState	1000efb0	undefined4 cm_HandleClientState(int param_1)	43
cm_HandleClientState2	1000efdb	undefined4 cm_HandleClientState2(undefined4 param_1, int param_2)	39
cm_HandleClientState3	1000f002	undefined4 cm_HandleClientState3(undefined4 param_1, int param_2)	19
cm_SetBroadcastInterval	1000f015	undefined4 cm_SetBroadcastInterval(undefined4 param_1, int param_2)	18
cm_Nop	1000f027	undefined4 cm_Nop(void)	3
cm_KillPlayer	1000f030	int cm_KillPlayer(void * player_data)	43
cm_SetNextAktion2	1000f080	undefined4 cm_SetNextAktion2(int param_1)	26
cm_SetNextAktion3	1000f0a0	undefined4 cm_SetNextAktion3(int param_1)	37
cm_ExRemoveObject	1000f0d0	int cm_ExRemoveObject(void * param_1, undefined1 * param_2)	197
cm_ExPlant	1000f1a0	undefined4 cm_ExPlant(int param_1, undefined1 * param_2)	327
cm_ExAllocThemaPredigt	1000f2f0	undefined4 cm_ExAllocThemaPredigt(void * param_1, undefined1 * param_2)	172
cm_ExSetGebBesitzer	1000f3b0	undefined4 cm_ExSetGebBesitzer(int command_data, undefined1 * result_ptr)	206
cm_ExSetGebUpgrade	1000f590	undefined4 cm_ExSetGebUpgrade(int param_1, undefined1 * param_2)	237
cm_ExFreeGeb	1000f680	undefined4 cm_ExFreeGeb(undefined4 param_1, undefined1 * param_2)	171
cm_ExEmployWorker	1000f730	undefined4 cm_ExEmployWorker(int param_1, undefined1 * param_2)	515
cm_AssignAmt	1000f940	bool cm_AssignAmt(int param_1)	22
cm_PerformAmtAction	1000f960	bool cm_PerformAmtAction(int param_1)	22
cm_AllocCharacter	1000f980	undefined4 cm_AllocCharacter(void * param_1, undefined1 * param_2)	335
cm_CreateBuilding	1000fb30	int cm_CreateBuilding(void * player_data, uint8_t * status_flag)	153
cm_Stub2	1000fbd0	undefined4 cm_Stub2(undefined4 param_1, undefined1 * param_2)	22
cm_Nop2	1000fc06	undefined4 cm_Nop2(void)	3
cm_HandleClientState4	1000fc10	undefined4 cm_HandleClientState4(int param_1, undefined1 * param_2)	308
cm_HandleClientState5	1000fd50	undefined4 cm_HandleClientState5(int param_1, undefined1 * param_2)	445
cm_Stub3	1000ff10	undefined4 cm_Stub3(undefined4 param_1, undefined1 * param_2)	22
cm_CheckPlayer	1000ff30	bool cm_CheckPlayer(int param_1, undefined1 * param_2)	41
cm_StartCutscene	1000ff60	int cm_StartCutscene(void * cutscene_data, uint8_t * status_flag)	82
cm_SetPlayerMoney	1000ffc0	int cm_SetPlayerMoney(void * player_data)	70
cm_SetPlayerTitle	10010010	int cm_SetPlayerTitle(void * player_data)	110
cm_SetPlayerSkill	100100a0	int cm_SetPlayerSkill(void * player_data)	159
cm_ZombieCommand	10010260	int cm_ZombieCommand(int param_1)	114
cm_AllocGraveyardWorker	10010310	int cm_AllocGraveyardWorker(int param_1)	52
cm_GetPlayerAmtId	10010350	int cm_GetPlayerAmtId(int param_1)	52
srv_HandlePlayerCommand	10010390	undefined4 srv_HandlePlayerCommand(int command_data)	262
cm_ExGetBuildingDataSize	100104a0	int cm_ExGetBuildingDataSize(void * building_data)	135
cm_ExValidateBuildingData	10010530	int cm_ExValidateBuildingData(void * building_data, int data_type)	113
cm_ExGetBuildingDataPtr	100105b0	int cm_ExGetBuildingDataPtr(void * building_data, int data_type, byte index)	329
cm_ExIterateBuildingData_callback	10010700	bool cm_ExIterateBuildingData_callback(undefined4 param_1, int param_2)	14
cm_ExIterateBuildingData	10010710	uint32_t cm_ExIterateBuildingData(void * callback_data, void * building_type_data, int start_offset, void * callback, int data_type)	320
cm_ExAllocGraveyard	10010850	int cm_ExAllocGraveyard(void * building_type_data, int count)	370
gv_AllocGraveyardField	100109d0	undefined4 * gv_AllocGraveyardField(byte * building_type_data)	832
cm_ExUpgradeGraveyard	10010d10	int cm_ExUpgradeGraveyard(void * graveyard_data)	570
cm_ExFreeGraveyard	10010f50	void cm_ExFreeGraveyard(void * graveyard_data)	66
cm_SetZombieData	10010fa0	int cm_SetZombieData(void * zombie_data)	525
cm_CreateZombie	100111b0	int cm_CreateZombie(void * zombie_data)	501
cm_UpdateZombieData	100113b0	int cm_UpdateZombieData(void * zombie_data)	390
cm_SetZombieOwner	10011540	int cm_SetZombieOwner(void * zombie_data)	288
cm_SetZombieState	10011660	int cm_SetZombieState(void * zombie_data)	297
cm_ZombieLogic	10011790	int cm_ZombieLogic(void * zombie_data)	242
cm_AllocGraveyardWorker	10011890	int cm_AllocGraveyardWorker(void * worker_data)	164
cm_ExMoveZombie	10011940	int cm_ExMoveZombie(void * zombie_data)	674
handleAllocGraveyardWorker2	10011bf0	uint32_t handleAllocGraveyardWorker2(void * worker_data)	1040
handleLoadGraveyardData	10012000	int handleLoadGraveyardData(void * file_handle, void * building_type_data)	728
gm_playerInit	100122e0	void gm_playerInit(int init_type, uint32_t player_id, uint16_t player_type, void * player_data)	346
fs_read_file_data	10012440	bool fs_read_file_data(void * buffer, int element_size, int element_count, void * file_data)	37
gm_loadPlayerData	10012470	int gm_loadPlayerData(void * file_handle, void * player_data)	857
gm_loadBuildingData	100127d0	int gm_loadBuildingData(void * file_handle)	282
gd_load_game_data	100128f0	int gd_load_game_data(void * file_handle)	1463
dyn_load_data	10012eb0	int dyn_load_data(void * file_handle)	884
load_player_and_building_data	10013230	int load_player_and_building_data(void * file_ptr)	2268
gs_LoadGameData	10013b10	int gs_LoadGameData(void * file_handle)	1361
ls_ID2Ptr	10014070	int ls_ID2Ptr(void)	491
srv_RecvGame	10014260	int srv_RecvGame(void * file_handle)	892
lb_ExPlayerlist	100145e0	int lb_ExPlayerlist(void * client_data, void * command_data)	209
lb_ExPlayerReadyStatus	100146c0	int lb_ExPlayerReadyStatus(void * client_data, void * command_data)	236
lb_ExPlayerHasJoined	100147b0	int lb_ExPlayerHasJoined(void * client_data, void * command_data)	670
lb_update_player_status	10014a50	int lb_update_player_status(void * client_data, void * command_data)	157
lb_forward_command	10014af0	int lb_forward_command(void * client_data, void * command_data)	247
lb_get_player_data	10014bf0	int lb_get_player_data(void * client_data, void * command_data)	163
lb_chat_message	10014ca0	int lb_chat_message(void * client_data, void * command_data)	265
lb_ExLobbyServerCommand	10014db0	int lb_ExLobbyServerCommand(void * client_slot, void * command)	267
plt_get_map	10014ee0	undefined * plt_get_map(uint map_id)	69
plt_find_free_slot	10014f30	int plt_find_free_slot(int plant_map, uint x_coord, uint y_coord)	74
plt_find_slot_by_coords	10014f80	int plt_find_slot_by_coords(int plant_map, int x_coord, int y_coord)	103
plt_is_slot_free	10014ff0	int plt_is_slot_free(void * plant_map, uint32_t x_coord, uint32_t y_coord, int size)	175
plt_set_slot	100150a0	int plt_set_slot(int plant_map, uint x_coord, uint y_coord, uint map_id, int plant_type)	257
res_get_data	100151b0	int res_get_data(int resource_id, void * resource_data)	41
sim_cit_create	100151e0	uint32_t sim_cit_create(void * game_data)	535
sim_cit_add_to_building	10015400	void sim_cit_add_to_building(void * building_data, void * citizen_data)	83
sim_cit_remove_from_building	10015460	void sim_cit_remove_from_building(void * citizen_data)	145
sim_CreateCitizen	10015500	void * sim_CreateCitizen(uint8_t creation_flags, uint32_t new_citizen_id, void * game_data_ptr, uint8_t citizen_gender, uint8_t citizen_age)	180
sim_UpdateCitizenAge	100155c0	int sim_UpdateCitizenAge(void * citizen_data, int days_to_add, int months_to_add, int years_to_add)	197
sim_SetCitizenData	10015690	void sim_SetCitizenData(void * citizen_data, uint8_t gender, uint32_t age, uint32_t birth_year)	41
gm_initObjectManufacturer	100156c0	void gm_initObjectManufacturer(void)	642
gm_open	10015950	int gm_open(char * game_path)	861
gd_load_game_data_2	10015cb0	void gd_load_game_data_2(void)	57
gd_load_game_data_3	10015cf0	void gd_load_game_data_3(void)	194
gd_load_game_data_4	10015dc0	int gd_load_game_data_4(int object_id)	55
gd_load_game_data_5	10015e00	void gd_load_game_data_5(void)	135
gm_getObjectByID	10015e90	int gm_getObjectByID(void * * building_data_ptr, void * * object_data_ptr, void * * alchemist_data_ptr, uint32_t id)	211
gd_load_game_data_7	10015f70	void gd_load_game_data_7(uint32_t game_data_id)	714
gm_getObjectFromList	10016240	undefined4 * gm_getObjectFromList(int list_id, uint object_id)	72
obj_get_next_from_list	10016290	undefined obj_get_next_from_list()	464
gm_findObject	10016460	int gm_findObject(int list_id, int filter_flags)	284
obj_management	100165a0	void obj_management(void)	37
handleRemoveObjectFromList	100165d0	int handleRemoveObjectFromList(void * list_ptr, uint32_t object_id)	155
handleNoop2	10016670	void handleNoop2(void)	1
obj_remove_from_list_by_id	10016680	int obj_remove_from_list_by_id(void * list_ptr, uint32_t object_id)	139
handleFreeObjectList	10016710	int handleFreeObjectList(void * list_ptr)	66
gm_allocObject	10016760	ushort * gm_allocObject(uint32_t parent_id, uint object_type, undefined4 flags)	930
gm_addObject	10016cd0	ushort * gm_addObject(uint32_t parent_id, uint object_id, int count)	272
gm_subObject	10016de0	int gm_subObject(uint32_t parent_id, uint32_t object_id, int count)	186
gm_removeObjectNoKill	10016ea0	int gm_removeObjectNoKill(uint32_t parent_id, uint32_t object_id, int count)	211
bld_getNext	10016f80	byte * bld_getNext(void)	346
gm_findObject2	100170e0	byte * gm_findObject2(int filter_flags)	267
gm_getFreeBuildingSlot	10017210	char * gm_getFreeBuildingSlot(void)	39
gm_freeBuilding	10017240	int gm_freeBuilding(void * building_data)	167
bld_manage	10017330	void bld_manage(void * building_data)	207
bld_manage2	10017400	void bld_manage2(void * building_data)	202
gm_allocBuilding	100174d0	byte * gm_allocBuilding(byte building_type, ushort owner_id)	959
bld_manage3	10017910	void bld_manage3(void * building_data)	145
bld_getType	100179b0	uint32_t bld_getType(uint32_t building_id)	108
bld_getPlayerBuilding	10017a70	char * bld_getPlayerBuilding(int player_id)	62
bld_isResidence	10017ab0	byte * bld_isResidence(byte * building_data)	74
bld_setOwner	10017b00	void bld_setOwner(void * building_data, uint16_t owner_id, uint32_t new_owner_id)	320
gm_allocRoom	10017c40	ushort * gm_allocRoom(byte * building_data, uint room_type)	742
obj_remove_from_list_4	10017f30	int obj_remove_from_list_4(void * building_data, uint32_t object_id)	35
obj_detach_from_parent	10017f60	void obj_detach_from_parent(void * object_data)	36
amt_remove_player_wrapper	10017f90	void amt_remove_player_wrapper(void * player_data)	23
gm_killPlayer	10017fb0	void gm_killPlayer(uint32_t player_id, int cleanup_type)	278
gm_resetPlayers	100180d0	void gm_resetPlayers(void)	81
gm_isPlayerInState	10018130	int gm_isPlayerInState(void * player_data)	32
gm_isPlayerInState2	10018150	int gm_isPlayerInState2(uint32_t state_id)	34
gm_getPlayerAttribute	100181a0	uint8_t gm_getPlayerAttribute(uint32_t player_id, int attribute_type)	87
gm_getPlayerClass	10018200	uint32_t gm_getPlayerClass(uint32_t player_type)	123
gm_getPlayerLevel	10018330	int gm_getPlayerLevel(uint32_t player_type)	276
gm_getRandomPlayerAttribute	10018450	uint8_t gm_getRandomPlayerAttribute(uint8_t base_value)	78
gm_getPlayerByID	100184a0	undefined2 * gm_getPlayerByID(int player_id)	56
gm_getPlayerResidence	100184e0	undefined2 * gm_getPlayerResidence(int player_data)	66
gm_changePlayerIdentity	10018530	uint32_t gm_changePlayerIdentity(uint32_t player_id_1, uint32_t player_id_2)	800
gm_allocPlayer	10018850	uint16_t gm_allocPlayer(uint32_t player_type, uint32_t father_id, uint32_t mother_id, void * player_data, void * building_data, uint8_t gender, uint32_t age, int init_type)	3689
bld_getItemCount	100196c0	int bld_getItemCount(uint32_t building_id, uint32_t item_id)	81
gm_calculateItemValue	10019720	float gm_calculateItemValue(uint32_t item_id, uint32_t quantity)	396
itm_management	100198b0	void itm_management(void * building_data)	355
bld_getObjectCount	10019a20	int bld_getObjectCount(void * building_data)	74
obj_management_3	10019a70	uint32_t obj_management_3(void * building_data)	102
gm_getPlayerSpouse	10019ae0	undefined2 * gm_getPlayerSpouse(undefined2 * player_data)	82
gm_getPlayerChild	10019b40	uint16_t gm_getPlayerChild(void * player_data)	62
gm_getPlayerParent	10019b80	int gm_getPlayerParent(void * player_data)	83
gm_getPlayerSibling	10019be0	int gm_getPlayerSibling(ushort player_id)	124
gm_getPlayerResidence2	10019c60	undefined2 * gm_getPlayerResidence2(int player_id)	98
gm_getBuildingItemCount	10019cd0	int gm_getBuildingItemCount(void * item_data, void * object_data)	48
bld_getInventorySize	10019d00	int bld_getInventorySize(void * building_data)	39
gm_isInventoryFull	10019d30	int gm_isInventoryFull(void * building_data, uint32_t item_id, int quantity)	407
bld_sell_item_to	10019ed0	uint32_t bld_sell_item_to(void * building_data, uint32_t item_id, uint32_t quantity)	395
bld_manage4	1001a060	void bld_manage4(void)	97
get_random_number	1001a0d0	int get_random_number(uint16_t max_value)	32
get_random_float	1001a0f0	float get_random_float(void)	22
get_random_float_in_range	1001a110	float get_random_float_in_range(void)	48
rand_srand	1001a140	void rand_srand(uint seed)	14
rand_seed	1001a150	void rand_seed(uint32_t seed)	12
CRT_closesocket	1001a160	thunk int CRT_closesocket(int s)	6
sendto	1001a166	thunk int sendto(int socket, void * buf, int len, int flags, void * to, int tolen)	6
bind	1001a16c	thunk int bind(int socket, void * addr, int addrlen)	6
CRT_htons	1001a172	thunk u_short CRT_htons(u_short hostshort)	6
CRT_htonl	1001a178	thunk u_long CRT_htonl(u_long hostlong)	6
setsockopt	1001a17e	thunk int setsockopt(int socket, int level, int optname, void * optval, int optlen)	6
socket	1001a184	thunk int socket(int af, int type, int protocol)	6
CRT_fclose	1001a18a	int CRT_fclose(void * file_handle)	49
CRT___fclose_lk	1001a1bb	int CRT___fclose_lk(FILE * file_ptr)	76
write_string_to_file	1001a207	int write_string_to_file(char * p_str, FILE * p_file)	78
open_file	1001a255	undefined4 open_file(undefined4 filename, undefined4 mode, undefined4 file_ptr)	49
open_file_wrapper	1001a286	void open_file_wrapper(undefined4 filename, undefined4 mode)	19
CRT_sprintf	1001a299	undefined4 CRT_sprintf(undefined1 * buffer, undefined4 format, ...)	82
CRT_filelength_wrapper	1001a2eb	long CRT_filelength_wrapper(int fd)	34
CRT_filelength	1001a30d	long CRT_filelength(int fd)	353
CRT_fseek	1001a46e	int CRT_fseek(FILE * stream, long offset, int origin)	44
CRT_fseek	1001a49a	int CRT_fseek(void * file_handle, int offset, int origin)	141
CRT_get_current_time	1001a527	char * CRT_get_current_time(void * timeptr)	25
CRT__strrchr	1001a540	char * CRT__strrchr(char * str, int character)	39
CRT_GetLocalTime	1001a567	void CRT_GetLocalTime(time_t * time)	220
CRT__onexit_init	1001a643	void CRT__onexit_init(void)	45
CRT_exit	1001a670	void CRT_exit(uint32_t exit_code)	17
CRT___exit	1001a681	void CRT___exit(int exit_code)	17
CRT__cexit	1001a692	void CRT__cexit(void)	15
CRT_atexit	1001a6a1	void CRT_atexit(uint32_t exit_code, int quick_exit, int quiet_mode)	163
CRT__lock	1001a746	void CRT__lock(void)	9
CRT__unlock	1001a74f	void CRT__unlock(void)	9
CRT__initterm	1001a758	void CRT__initterm(void * * start_ptr, void * * end_ptr)	26
CRT_get_error_code	1001a772	void CRT_get_error_code(int error)	115
CRT__errno	1001a7e5	int * CRT__errno(void)	9
CRT___doserrno	1001a7ee	int * CRT___doserrno(void)	9
CRT__malloc	1001a7f7	void * CRT__malloc(size_t size)	18
CRT___nh_malloc	1001a809	void * CRT___nh_malloc(size_t size, int nh_flag)	44
CRT__heap_alloc_base	1001a835	void CRT__heap_alloc_base(size_t size)	231
CRT_unlock_heap	1001a89c	void CRT_unlock_heap(void)	9
CRT_unlock_heap	1001a8fb	void CRT_unlock_heap(void)	9
CRT_fwrite	1001a931	size_t CRT_fwrite(void * buffer, size_t size, size_t count, FILE * stream)	47
CRT_fwrite	1001a960	uint32_t CRT_fwrite(void * buffer, uint32_t element_size, uint32_t element_count, void * file_handle)	266
CRT_fread	1001aa6a	uint32_t CRT_fread(void * buffer, uint32_t element_size, uint32_t element_count, void * file_handle)	47
CRT_fread_nolock	1001aa99	uint32_t CRT_fread_nolock(void * buffer, uint32_t element_size, uint32_t element_count, void * file_handle)	232
CRT_free	1001ab81	void CRT_free(void * ptr)	215
CRT_unlock_heap	1001abeb	void CRT_unlock_heap(void)	9
CRT_unlock_heap	1001ac43	void CRT_unlock_heap(void)	9
stack_unwind_helper	1001ac70	void stack_unwind_helper(void)	47
CRT_flush	1001ac9f	int CRT_flush(void * file_handle)	46
CRT_flush_buffer	1001accd	int CRT_flush_buffer(void * file_handle)	92
CRT_flush_all_wrapper	1001ad29	undefined CRT_flush_all_wrapper(void)	9
CRT_flush_all	1001ad32	int CRT_flush_all(int operation_type)	164
CRT_fputc	1001add6	uint32_t CRT_fputc(uint32_t character, void * file_handle)	59
CRT__strncpy	1001ae20	char * CRT__strncpy(char * _Dest, char * _Source, int _Count)	254
CRT__strchr	1001af30	char * CRT__strchr(char * _Str, int _Val)	193
CRT__strstr	1001aff0	char * CRT__strstr(char * _Str, char * _SubStr)	128
CRT_startup	1001b070	void CRT_startup(void)	23
CRT_Startup2	1001b088	void CRT_Startup2(void)	56
CRT_toupper	1001b0c0	int CRT_toupper(int _C)	111
CRT__toupper_l	1001b12f	int CRT__toupper_l(int _C, int _Locale)	204
CRT_memmove	1001b200	undefined4 * CRT_memmove(undefined4 * destination, undefined4 * source, uint count)	664
rand_seed_internal	1001b535	void rand_seed_internal(uint32_t seed_val)	13
CRT__rand	1001b542	int CRT__rand(void)	34
CRT__ftol	1001b564	long CRT__ftol(double value)	39
CRT_Startup3	1001b58b	int CRT_Startup3(char * format_string)	65
CRT_realloc_internal	1001b5cc	byte * CRT_realloc_internal(byte * old_ptr, uint new_size)	781
CRT_unlock_heap	1001b757	void CRT_unlock_heap(void)	9
CRT_unlock_heap	1001b8a5	void CRT_unlock_heap(void)	11
DllMain	1001b8fb	BOOL DllMain(HINSTANCE hinstDLL, DWORD fdwReason, LPVOID lpvReserved)	217
entry	1001b9d4	BOOL entry(HINSTANCE hinstDLL, DWORD fdwReason, LPVOID lpvReserved)	157
CRT___amsg_exit	1001ba71	void CRT___amsg_exit(int exit_code)	48
CRT_init_streams	1001baa4	undefined CRT_init_streams(void)	168
CRT_lock_stream_by_ptr	1001bb60	void CRT_lock_stream_by_ptr(FILE * stream)	47
CRT_lock_stream_by_id	1001bb8f	void CRT_lock_stream_by_id(int stream_id, FILE * stream)	35
CRT__unlock_file	1001bbb2	void CRT__unlock_file(int * _File)	47
CRT__unlock_fileno	1001bbe1	void CRT__unlock_fileno(int _FileNo)	35
CRT__close	1001bc04	int CRT__close(int fd)	93
CRT__close_nolock	1001bc61	int CRT__close_nolock(int fd)	131
CRT___freebuf	1001bce4	void CRT___freebuf(FILE * file_ptr)	43
CRT_init_stream	1001bd0f	uint32_t CRT_init_stream(void * file_ptr)	141
CRT_flush_and_reset_buffer	1001bd9c	void CRT_flush_and_reset_buffer(int status, void * file_ptr)	42
CRT__strlen	1001bdd0	int CRT__strlen(char * _Str)	123
CRT_fopen	1001be4b	undefined4 * CRT_fopen(LPCSTR file_descriptor, char * mode_string, uint file_handle_ptr, undefined4 * file_struct_ptr)	368
CRT__getstream	1001bfbb	FILE * CRT__getstream(void)	200
CRT_fputc_nolock	1001c083	uint32_t CRT_fputc_nolock(uint32_t character, void * file_ptr)	280
CRT_printf_core	1001c19b	int CRT_printf_core(void * file_ptr, char * format_string, void * arg_list)	1825
CRT_printf_putc	1001c8dc	void CRT_printf_putc(uint32_t character, void * file_ptr, int * chars_written)	53
CRT_printf_putc_n	1001c911	void CRT_printf_putc_n(uint32_t character, int count, void * file_ptr, int * chars_written)	49
CRT_printf_puts	1001c942	void CRT_printf_puts(char * string, int length, void * file_ptr, int * chars_written)	56
CRT_printf_get_int_arg	1001c97a	uint32_t CRT_printf_get_int_arg(void * arg_list)	13
CRT_printf_get_int64_arg	1001c987	uint64_t CRT_printf_get_int64_arg(void * arg_list)	16
CRT_printf_get_int32_arg	1001c997	uint32_t CRT_printf_get_int32_arg(void * arg_list)	14
CRT_init_file_descriptors	1001c9a5	void CRT_init_file_descriptors(void)	444
CRT_shutdown	1001cb61	void CRT_shutdown(void)	84
CRT_lseek	1001cbb5	uint32_t CRT_lseek(uint32_t file_descriptor, uint32_t offset, uint32_t origin)	101
CRT_lseek_nolock	1001cc1a	uint32_t CRT_lseek_nolock(uint32_t file_descriptor, int32_t offset, uint32_t move_method)	115
format_datetime	1001cc8d	char * format_datetime(int * datetime_data)	202
format_number	1001cd57	char * format_number(char * buffer, int number)	40
time_to_tm	1001cd7f	int * time_to_tm(int * p_time)	352
tm_to_time	1001cedf	int tm_to_time(int year, int month, int day, int hour, int minute, int second, int is_dst)	194
CRT_init	1001cfa1	void CRT_init(void)	41
CRT_deinit	1001cfca	void CRT_deinit(void)	108
CRT_lock_resource	1001d036	void CRT_lock_resource(int resource_id)	97
CRT__unlock	1001d097	void CRT__unlock(int _LockNum)	21
tls_init	1001d0ac	int tls_init(void)	84
tls_deinit	1001d100	void tls_deinit(void)	30
tls_init_block	1001d11e	void tls_init_block(void * tls_block_ptr)	19
CRT_get_tls_block	1001d131	void * CRT_get_tls_block(void)	103
CRT_free_tls_block	1001d198	void CRT_free_tls_block(void * tls_block)	160
new_handler	1001d238	int new_handler(uint32_t size)	27
get_linked_os_version	1001d253	void get_linked_os_version(OSVERSIONINFO * version_info)	45
mem_select_heap_implementation	1001d280	int mem_select_heap_implementation(void)	328
mem__heap_init	1001d3c8	int mem__heap_init(void)	93
mem_heap_term	1001d425	void mem_heap_term(void)	168
mem_init_custom_heap	1001d4cd	int mem_init_custom_heap(int max_size)	72
mem_find_custom_heap_block	1001d515	void * mem_find_custom_heap_block(void * address)	43
mem_free_custom_heap_block	1001d540	void mem_free_custom_heap_block(void * block_info, void * mem_ptr)	809
mem_HeapAllocBlock	1001d869	void * mem_HeapAllocBlock(size_t size)	777
mem_HeapExtend	1001db72	void * mem_HeapExtend(void)	177
mem_HeapAllocPage	1001dc23	int mem_HeapAllocPage(void * heap_info)	251
mem_HeapReallocBlock	1001dd1e	int mem_HeapReallocBlock(void * heap_info, void * mem_ptr, size_t new_size)	758
virt_heap_alloc	1001e014	void * virt_heap_alloc(void)	324
virt_heap_free	1001e158	void virt_heap_free(void * heap_ptr)	86
virt_heap_free_pages	1001e1ae	void virt_heap_free_pages(int count)	194
virt_heap_get_block_info	1001e270	int virt_heap_get_block_info(void * mem_ptr, void * * heap_info_ptr, void * * page_base_ptr)	87
virt_heap_free_block	1001e2c7	void virt_heap_free_block(void * heap_info, void * page_base, void * mem_ptr)	69
virt_heap_alloc_block	1001e30c	void * virt_heap_alloc_block(size_t size)	520
virt_heap_alloc_from_block	1001e514	void * virt_heap_alloc_from_block(void * block_info, size_t offset, size_t size)	292
virt_heap_realloc_block	1001e638	int virt_heap_realloc_block(void * heap_info, void * page_info, void * mem_ptr, size_t new_size)	169
CRT___global_unwind2	1001e6e4	void CRT___global_unwind2(void * frame)	32
CRT_global_unwind_helper	1001e704	undefined4 CRT_global_unwind_helper(int param_1, undefined4 param_2, undefined4 param_3, undefined4 * param_4)	34
CRT___local_unwind2	1001e726	void CRT___local_unwind2(void * frame, int state)	104
save_exception_context	1001e7ba	void save_exception_context(void * exception_record_ptr, void * context_ptr, void * ebp_ptr)	24
CRT___except_handler3	1001e7dc	undefined4 CRT___except_handler3(int param_1, void * param_2, undefined4 param_3)	189
CRT___seh_longjmp_unwind	1001e899	void CRT___seh_longjmp_unwind(void * exception_info)	27
CRT_write	1001e8b4	uint32_t CRT_write(uint32_t file_descriptor, void * buffer, uint32_t count)	101
CRT_write_nolock	1001e919	int CRT_write_nolock(uint32_t file_descriptor, void * buffer, uint32_t count)	395
CRT_memmove	1001eab0	undefined4 * CRT_memmove(undefined4 * destination, undefined4 * source, uint count)	664
CRT_fgetc	1001ede5	uint32_t CRT_fgetc(void * file_ptr)	220
CRT_read	1001eec1	uint32_t CRT_read(uint32_t file_descriptor, void * buffer, uint32_t count)	101
CRT_read_nolock	1001ef26	int CRT_read_nolock(uint32_t file_descriptor, void * buffer, uint32_t count)	473
CRT_flush_file_buffers	1001f0ff	uint32_t CRT_flush_file_buffers(uint32_t file_descriptor)	147
CRT_Startup10	1001f192	void CRT_Startup10(void)	18
CRT_Startup11	1001f1a4	int CRT_Startup11(void)	62
CRT__check_processor_features	1001f1e2	void CRT__check_processor_features(void)	41
CRT_atof	1001f20b	double CRT_atof(char * _Str)	90
CRT_atof_cleanup	1001f265	undefined CRT_atof_cleanup(char * param_1)	78
CRT_check_for_overflow	1001f2b3	undefined4 CRT_check_for_overflow(double * param_1)	24
CRT___fassign	1001f2cb	void CRT___fassign(int flag, void * dst, void * src)	62
CRT__gcvt	1001f309	char * CRT__gcvt(double _Value, int _NbrOfDigits, char * _DstBuf)	97
CRT_gcvt_s	1001f36a	int CRT_gcvt_s(char * _Buffer, int _SizeInBytes, double _Value, int _NbrOfDigits)	194
CRT__fcvt	1001f42c	char * CRT__fcvt(double _Value, int _NbrOfDigits, int * _Dec, int * _Sign)	85
CRT_fcvt_s	1001f481	int CRT_fcvt_s(char * _Buffer, int _SizeInBytes, double _Value, int _NbrOfDigits, int * _Dec, int * _Sign)	167
CRT__ecvt	1001f528	char * CRT__ecvt(double _Value, int _NbrOfDigits, int * _Dec, int * _Sign)	147
CRT___cfltcvt	1001f5bb	int CRT___cfltcvt(double * arg1, char * arg2, size_t arg3, int arg4, int arg5, int arg6)	81
CRT_strcpy	1001f60c	char * CRT_strcpy(char * _Dest, char * _Source)	37
CRT___crtLCMapStringA	1001f631	int CRT___crtLCMapStringA(LCID lcid, DWORD flags, LPCSTR src, int srclen, LPWSTR dst, int dstlen, UINT codepage, BOOL error_flag)	511
CRT_get_char_property	1001f855	ushort CRT_get_char_property(void * this, wchar_t c, int type, int mask)	117
CRT_strcpy_optimized	1001f8d0	uint * CRT_strcpy_optimized(uint * dest_ptr, uint * src_ptr)	7
CRT_strcat	1001f8e0	char * CRT_strcat(char * _Dest, char * _Source)	224
CRT__init_environ	1001f9c0	void CRT__init_environ(void)	185
CRT__init_argv	1001fa79	void CRT__init_argv(void)	153
CRT_parse_command_line	1001fb12	void CRT_parse_command_line(char * cmdline, char * * argv, char * * envp, int * argc, int * env_size)	436
CRT___setenvp	1001fcc6	void CRT___setenvp(void)	306
handle_runtime_error	1001fdf8	void handle_runtime_error(uint error_code)	57
display_runtime_error	1001fe31	int display_runtime_error(int * func)	339
CRT__calloc_base	1001ff84	void CRT__calloc_base(int num)	289
CRT_unlock_heap	1002001d	void CRT_unlock_heap(void)	9
CRT_unlock_heap	100200a6	undefined CRT_unlock_heap(void)	9
CRT_unlock_file_handles	10020135	undefined CRT_unlock_file_handles(void)	13
CRT_alloc_handle	10020142	uint CRT_alloc_handle(void)	291
CRT_set_handle	10020265	undefined4 CRT_set_handle(uint param_1, HANDLE param_2)	124
CRT_free_handle	100202e1	undefined4 CRT_free_handle(uint param_1)	127
CRT_get_handle	10020360	undefined4 CRT_get_handle(uint param_1)	66
CRT_lock_handle	100203a2	undefined CRT_lock_handle(uint param_1)	95
CRT_unlock_handle	10020401	undefined CRT_unlock_handle(uint param_1)	34
CRT_is_char_device	10020423	byte CRT_is_char_device(uint param_1)	41
CRT_open	1002044c	uint CRT_open(LPCSTR param_1, uint param_2, uint param_3, uint param_4)	719
CRT_alloc_buffer	1002071b	undefined CRT_alloc_buffer(undefined4 * param_1)	68
CRT_wctomb	1002075f	int CRT_wctomb(char * _MbCh, int _WCh)	89
CRT__wctomb_l	100207b8	int CRT__wctomb_l(char * _MbCh, int _WCh, int _Locale)	105
CRT___aulldiv	10020830	undefined8 CRT___aulldiv(uint param_1, uint param_2, uint param_3, uint param_4)	104
CRT___aullrem	100208a0	ulonglong CRT___aullrem(ulonglong a, ulonglong b)	117
time_init	10020915	undefined time_init(void)	46
CRT__tzset	10020943	void CRT__tzset(void)	647
time_is_dst_locked	10020bca	int time_is_dst_locked(void)	33
CRT__daylight	10020beb	int CRT__daylight(void)	428
time_calculate_dst_date	10020d97	undefined time_calculate_dst_date(int is_start_date, int is_fixed_date, uint year, int month, int week, int day_of_week, int day, int hour, int minute, int second, int millisecond)	320
CRT_gmtime	10020ed7	int * CRT_gmtime(int * _Time)	266
CRT_atoi	10020fe1	int CRT_atoi(char * _Str)	23
CRT_strtol	10020ff8	long CRT_strtol(void * this, char * _Str, char * * _EndPtr, int _Radix)	517
CRT__strncmp	10021200	int CRT__strncmp(char * _Str1, char * _Str2, int _MaxCount)	56
CRT__memset	10021240	void * CRT__memset(void * _Dst, int _Val, size_t _Size)	88
CRT_bitwise_select	10021298	uint CRT_bitwise_select(uint source1, uint mask)	53
CRT_bitwise_select_masked	100212cd	undefined CRT_bitwise_select_masked(uint source, uint mask)	22
CRT_bitwise_permute	100212e3	uint CRT_bitwise_permute(uint original_value)	146
CRT_bitwise_inverse_permute	10021375	uint CRT_bitwise_inverse_permute(uint permuted_value)	137
CRT_tolower	100213fe	int CRT_tolower(int _C)	111
CRT__tolower_l	1002146d	int CRT__tolower_l(void * this, int _C, int _Locale)	203
CRT_bitwise_is_range_clear	10021538	undefined4 CRT_bitwise_is_range_clear(int bitfield, int start_index)	73
CRT_bitwise_set_and_propagate	10021581	undefined CRT_bitwise_set_and_propagate(int bitfield, int bit_index)	86
CRT_bitwise_clear_range_and_propagate	100215d7	undefined4 CRT_bitwise_clear_range_and_propagate(int bitfield, int start_index)	140
memcpy_12_bytes	10021663	undefined memcpy_12_bytes(int param_1, undefined4 * param_2)	27
memset_12_bytes_zero	1002167e	undefined memset_12_bytes_zero(undefined4 * param_1)	12
memcmp_internal	1002168a	undefined4 memcmp_internal(int * param_1)	27
bitstream_copy	100216a5	undefined bitstream_copy(uint * dest_buffer, uint num_bits_to_copy)	141
float_conversion	10021732	undefined4 float_conversion(ushort * param_1, uint * param_2, int * param_3)	364
float_conversion_2	1002189e	undefined float_conversion_2(ushort * param_1, uint * param_2)	22
float_conversion_3	100218b4	undefined float_conversion_3(ushort * param_1, uint * param_2)	22
float_conversion_4	100218ca	undefined float_conversion_4(uint * param_1, undefined4 param_2)	45
float_conversion_5	100218f7	undefined float_conversion_5(uint * param_1, undefined4 param_2)	45
format_float	10021924	undefined format_float(char * param_1, int param_2, int param_3)	119
get_float_components	1002199b	int * get_float_components(undefined4 param_1, undefined4 param_2, int * param_3, uint * param_4)	92
float_conversion_6	100219f7	undefined float_conversion_6(uint * param_1, uint * param_2)	182
CRT___fptrap	10021aad	void CRT___fptrap(void)	9
CRT__strcmp	10021ac0	int CRT__strcmp(char * _Str1, char * _Str2)	129
custom_strtok	10021b50	int custom_strtok(byte * input_str, byte * delimiter_str)	62
custom_strtok_ptr	10021b90	byte * custom_strtok_ptr(byte * input_str, byte * delimiter_str)	58
CRT_get_string_type	10021bca	BOOL CRT_get_string_type(DWORD dwInfoType, LPCSTR lpSrcStr, int cchSrc, LPWORD lpCharType)	318
CRT__setmbcp	10021d13	int CRT__setmbcp(int codepage)	429
CRT___getmbcp_from_locale	10021ec0	int CRT___getmbcp_from_locale(int category)	74
get_lang_id_from_codepage	10021f0a	LANGID get_lang_id_from_codepage(int codepage)	51
CRT_reset_locale_info	10021f3d	void CRT_reset_locale_info(void)	41
CRT_init_ctype	10021f66	void CRT_init_ctype(void)	389
CRT_Startup25	100220eb	undefined CRT_Startup25(void)	28
show_message_box	10022107	int show_message_box(undefined4 text, undefined4 caption, undefined4 type)	137
CRT_chsize	10022190	int CRT_chsize(uint32_t param_1, int param_2)	293
CRT__atoi_l	100222b5	int CRT__atoi_l(void * this, char * _Str, int _Locale)	139
CRT_getenv	10022340	char * CRT_getenv(char * _VarName)	125
CRT___add_with_carry	100223bd	undefined4 CRT___add_with_carry(uint operand1, uint operand2, uint * result_ptr)	33
CRT___add_12	100223de	undefined CRT___add_12(uint * param_1, uint * param_2)	94
CRT_lshl_96	1002243c	undefined CRT_lshl_96(uint * value)	46
CRT_lshr_96	1002246a	undefined CRT_lshr_96(uint * value)	45
hash_function	10022497	undefined hash_function(char * param_1, int param_2, uint * param_3)	199
CRT__atof_l	1002255e	double CRT__atof_l(char * _Str, int _Locale)	1185
float_conversion_13	10022a2f	undefined4 float_conversion_13(uint param_1, uint param_2, uint param_3, int param_4, byte param_5, short * param_6)	659
custom_strcmp	10022cd0	int custom_strcmp(void * this, byte * param_1, byte * param_2)	208
CRT__strnicmp_l	10022da0	void * CRT__strnicmp_l(byte * param_1, char * param_2, void * param_3)	257
CRT_Startup26	10022ea1	int CRT_Startup26(uint param_1, int param_2)	97
CRT___mbsnbicoll	10022f44	int CRT___mbsnbicoll(char * s1, char * s2, size_t n)	63
CRT__init_wide_environ	10022f83	int CRT__init_wide_environ(void)	110
float_conversion_14	10022ff1	undefined float_conversion_14(int * param_1, int * param_2)	544
float_conversion_15	10023211	undefined float_conversion_15(int * param_1, uint param_2, int param_3)	124
float_conversion_16	1002328d	int float_conversion_16(LCID param_1, DWORD param_2, byte * param_3, int param_4, byte * param_5, int param_6, UINT param_7)	597
CRT_strnlen	1002350a	int CRT_strnlen(char * _Str, int _MaxCount)	43
CRT_putenv	10023535	int CRT_putenv(char * _EnvString)	391
CRT__findenv	100236bc	char * CRT__findenv(char * _VarName, int * _Offset)	88
CRT__clone_environ	10023714	int CRT__clone_environ(void)	103
CRT__strchr_l	1002377b	char * CRT__strchr_l(char * _Str, int _Val, int _Locale)	151
CRT__strdup	10023812	char * CRT__strdup(char * _Src)	43
RtlUnwind	10023840	thunk void RtlUnwind(PVOID TargetFrame, PVOID TargetIp, PEXCEPTION_RECORD ExceptionRecord, PVOID ReturnValue)	6