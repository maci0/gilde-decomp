# zlib

`server.dll` statically links again `zlib-1.1.3`
https://zlib.net/fossils/zlib-1.1.3.tar.gz

Below the matched functions and their origin


| Function | Address | Decompilation | Confidence | Description | Notes |
|---|---|---|---|---|---|
| `zlib_adler32` | `0x10001000` | 100% | High | See zlib documentation. | Statically linked. From adler32.c, line 33. |
| `zlib_crc32` | `0x100011f0` | 100% | High | See zlib documentation. | Statically linked. From crc32.c, line 186. |
| `zlib_deflateInit2_` | `0x10001330` | 100% | High | See zlib documentation. | Statically linked. From deflate.c, line 204. |
| `zlib_deflateReset` | `0x10001530` | 100% | High | See zlib documentation. | Statically linked. From deflate.c, line 288. |
| `zlib_deflate` | `0x100015b0` | 100% | High | See zlib documentation. | Statically linked. From deflate.c, line 388. |
| `zlib_deflateEnd` | `0x10001910` | 100% | High | See zlib documentation. | Statically linked. From deflate.c, line 508. |
| `zlib_deflate_stored` | `0x10001a60` | 100% | High | See zlib documentation. | Statically linked. From deflate.c, line 681. |
| `zlib_fill_window` | `0x10001bc0` | 100% | High | See zlib documentation. | Statically linked. From deflate.c, line 868. |
| `zlib_read_buf` | `0x10001cf0` | 100% | High | See zlib documentation. | Statically linked. From deflate.c, line 365. |
| `zlib_parseGzipHeader` | `0x100036d0` | 100% | High | See zlib documentation. | Statically linked. From gzio.c, line 186. |
| `zlib_getByte` | `0x10003820` | 100% | High | See zlib documentation. | Statically linked. From gzio.c, line 161. |
| `zlib_closeFile` | `0x100038a0` | 100% | High | See zlib documentation. | Statically linked. From gzio.c, line 455. |
| `zlib_readFromStream` | `0x10003960` | 100% | High | See zlib documentation. | Statically linked. From gzio.c, line 293. |
| `zlib_writeToStream` | `0x10003b90` | 100% | High | See zlib documentation. | Statically linked. From gzio.c, line 365. |
| `zlib_getLong` | `0x10003c50` | 100% | High | See zlib documentation. | Statically linked. From gzio.c, line 485. |
| `zlib_closeStream` | `0x10003ca0` | 100% | High | See zlib documentation. | Statically linked. From gzio.c, line 455. |
| `zlib_putLong` | `0x10003cf0` | 100% | High | See zlib documentation. | Statically linked. From gzio.c, line 474. |
| `zlib_inflateReset` | `0x10003d20` | 100% | High | See zlib documentation. | Statically linked. From inflate.c, line 65. |
| `zlib_inflateInit2_` | `0x10003da0` | 100% | High | See zlib documentation. | Statically linked. From inflate.c, line 88. |
| `zlib_inflate` | `0x10003e40` | 100% | High | See zlib documentation. | Statically linked. From inflate.c, line 153. |
| `zlib_inflateEnd` | `0x10004b40` | 100% | High | See zlib documentation. | Statically linked. From inflate.c, line 76. |
| `zlib_tr_init` | `0x10004b80` | 100% | High | See zlib documentation. | Statically linked. From trees.c, line 505. |
| `zlib_inflate_codes` | `0x10004bc0` | 100% | High | See zlib documentation. | Statically linked. From infcodes.c, line 101. |
| `zlib_inflate_trees_free` | `0x10005370` | 100% | High | See zlib documentation. | Statically linked. From inftrees.c, line 418. |
| `zlib_inflate_fast` | `0x10005390` | 100% | High | See zlib documentation. | Statically linked. From inffast.c, line 28. |
| `zlib_inflate_blocks_reset` | `0x10005720` | 100% | High | See zlib documentation. | Statically linked. From infblock.c, line 158. |
| `zlib_inflate_blocks_free` | `0x10005770` | 100% | High | See zlib documentation. | Statically linked. From infblock.c, line 426. |
| `zlib_inflate_blocks_new` | `0x100057c0` | 100% | High | See zlib documentation. | Statically linked. From infblock.c, line 178. |
| `zlib_inflate_blocks` | `0x100058d0` | 100% | High | See zlib documentation. | Statically linked. From infblock.c, line 201. |
| `zlib_inflate_trees_dynamic` | `0x10005d00` | 100% | High | See zlib documentation. | Statically linked. From inftrees.c, line 353. |
| `zlib_huft_build` | `0x10005db0` | 100% | High | See zlib documentation. | Statically linked. From inftrees.c, line 88. |
| `zlib_inflate_trees_bits` | `0x10006280` | 100% | High | See zlib documentation. | Statically linked. From inftrees.c, line 329. |
| `zlib_inflate_trees_fixed` | `0x10006410` | 100% | High | See zlib documentation. | Statically linked. From inftrees.c, line 438. |
| `zlib_inflate_flush` | `0x10006440` | 100% | High | See zlib documentation. | Statically linked. From infutil.c, line 25. |
| `zlib_ct_init` | `0x10006ec0` | 100% | High | See zlib documentation. | Statically linked. From trees.c, line 505. |
| `zlib_tr_tally` | `0x10006f40` | 100% | High | See zlib documentation. | Statically linked. From trees.c, line 813. |
| `zlib_tr_flush_block` | `0x10006fb0` | 100% | High | See zlib documentation. | Statically linked. From trees.c, line 861. |
| `zlib_ct_tally` | `0x10007050` | 100% | High | See zlib documentation. | Statically linked. From trees.c, line 813. |
| `zlib_bi_flush` | `0x100072b0` | 100% | High | See zlib documentation. | Statically linked. From trees.c, line 1014. |
| `zlib_build_tree` | `0x100074a0` | 100% | High | See zlib documentation. | Statically linked. From trees.c, line 678. |
| `zlib_pqdownheap` | `0x100076e0` | 100% | High | See zlib documentation. | Statically linked. From trees.c, line 573. |
| `zlib_gen_codes` | `0x100077c0` | 100% | High | See zlib documentation. | Statically linked. From trees.c, line 644. |
| `zlib_gen_bitlen` | `0x100079f0` | 100% | High | See zlib documentation. | Statically linked. From trees.c, line 598. |
| `zlib_build_static_trees` | `0x10007a70` | 100% | High | See zlib documentation. | Statically linked. From trees.c, line 505. |
| `zlib_scan_tree` | `0x10007ae0` | 100% | High | See zlib documentation. | Statically linked. From trees.c, line 724. |
| `zlib_send_tree` | `0x10007bd0` | 100% | High | See zlib documentation. | Statically linked. From trees.c, line 765. |
| `zlib_send_codes` | `0x10007e40` | 100% | High | See zlib documentation. | Statically linked. From trees.c, line 914. |
| `zlib_send_all_trees` | `0x100083c0` | 100% | High | See zlib documentation. | Statically linked. From trees.c, line 833. |
| `zlib_build_bl_tree` | `0x10008800` | 100% | High | See zlib documentation. | Statically linked. From trees.c, line 801. |
| `zlib_bi_reverse` | `0x10008880` | 100% | High | See zlib documentation. | Statically linked. From trees.c, line 997. |
| `zlib_bi_windup` | `0x100088a0` | 100% | High | See zlib documentation. | Statically linked. From trees.c, line 1029. |
| `zlib_bi_align` | `0x10008930` | 100% | High | See zlib documentation. | Statically linked. From trees.c, line 850. |
| `zlib_tr_stored_block` | `0x100089b0` | 100% | High | See zlib documentation. | Statically linked. From trees.c, line 943. |
| `zlib_write_to_buffer` | `0x10001860` | 100% | High | See zlib documentation. | Statically linked. From deflate.c, line 62. |
| `zlib_flush_buffer` | `0x10001890` | 100% | High | See zlib documentation. | Statically linked. From deflate.c, line 75. |
| `zlib_reset_data` | `0x100019c0` | 100% | High | See zlib documentation. | Statically linked. From deflate.c, line 299. |
| `zlib_zcalloc` | `0x100092e0` | 100% | High | See zlib documentation. | Statically linked. From zutil.c, line 264. |
