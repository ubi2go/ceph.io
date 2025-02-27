---
title: "v10.2.6 Jewel released"
date: "2017-03-08"
author: "TheAnalyst"
tags:
  - "release"
  - "jewel"
---

This point release fixes several important bugs in RBD mirroring, RGW multi-site, CephFS, and RADOS.

We recommend that all v10.2.x users upgrade.

For more detailed information, see [the complete changelog](http://docs.ceph.com/docs/master/_downloads/v10.2.6.txt) .

## **OSDs No Longer Send ENXIO by Default**

In previous versions, if a client sent an op to the wrong OSD, the OSD would reply with ENXIO. The rationale here is that the client or OSD is clearly buggy and we want to surface the error as clearly as possible. We now only send the ENXIO reply if the osd\_enxio\_on\_misdirected\_op option is enabled (it's off by default). This means that a VM using librbd that previously would have gotten an EIO and gone read-only will now see a blocked/hung IO instead.

# Other Notable Changes

- build/ops: add hostname sanity check to run-{c}make-check.sh ([issue#18134](http://tracker.ceph.com/issues/18134), [pr#12302](http://github.com/ceph/ceph/pull/12302), Nathan Cutler)
- build/ops: add ldap lib to rgw lib deps based on build config ([issue#17313](http://tracker.ceph.com/issues/17313), [pr#13183](http://github.com/ceph/ceph/pull/13183), Nathan Cutler)
- build/ops: ceph-create-keys loops forever ([issue#17753](http://tracker.ceph.com/issues/17753), [pr#11884](http://github.com/ceph/ceph/pull/11884), Alfredo Deza)
- build/ops: ceph daemons DUMPABLE flag is cleared by setuid preventing coredumps ([issue#17650](http://tracker.ceph.com/issues/17650), [pr#11736](http://github.com/ceph/ceph/pull/11736), Patrick Donnelly)
- build/ops: fixed compilation error when --with-radowsgw=no ([issue#18512](http://tracker.ceph.com/issues/18512), [pr#12729](http://github.com/ceph/ceph/pull/12729), Pan Liu)
- build/ops: fixed the issue when --disable-server, compilation fails. ([issue#18120](http://tracker.ceph.com/issues/18120), [pr#12239](http://github.com/ceph/ceph/pull/12239), Pan Liu)
- build/ops: fix undefined crypto references with --with-xio ([issue#18133](http://tracker.ceph.com/issues/18133), [pr#12296](http://github.com/ceph/ceph/pull/12296), Nathan Cutler)
- build/ops: install-deps.sh based on /etc/os-release ([issue#18466](http://tracker.ceph.com/issues/18466), [issue#18198](http://tracker.ceph.com/issues/18198), [pr#12405](http://github.com/ceph/ceph/pull/12405), Jan Fajerski, Nitin A Kamble, Nathan Cutler)
- build/ops: Remove the runtime dependency on lsb\_release ([issue#17425](http://tracker.ceph.com/issues/17425), [pr#11875](http://github.com/ceph/ceph/pull/11875), John Coyle, Brad Hubbard)
- build/ops: rpm: /etc/ceph/rbdmap is packaged with executable access rights ([issue#17395](http://tracker.ceph.com/issues/17395), [pr#11855](http://github.com/ceph/ceph/pull/11855), Ken Dreyer)
- build/ops: selinux: Allow ceph to manage tmp files ([issue#17436](http://tracker.ceph.com/issues/17436), [pr#13048](http://github.com/ceph/ceph/pull/13048), Boris Ranto)
- build/ops: systemd: Restart Mon after 10s in case of failure ([issue#18635](http://tracker.ceph.com/issues/18635), [pr#13058](http://github.com/ceph/ceph/pull/13058), Wido den Hollander)
- build/ops: systemd restarts Ceph Mon to quickly after failing to start ([issue#18635](http://tracker.ceph.com/issues/18635), [pr#13184](http://github.com/ceph/ceph/pull/13184), Wido den Hollander)
- ceph-disk: fix flake8 errors ([issue#17898](http://tracker.ceph.com/issues/17898), [pr#11976](http://github.com/ceph/ceph/pull/11976), Ken Dreyer)
- cephfs: fuse client crash when adding a new osd ([issue#17270](http://tracker.ceph.com/issues/17270), [pr#11860](http://github.com/ceph/ceph/pull/11860), John Spray)
- cli: ceph-disk: convert none str to str before printing it ([issue#18371](http://tracker.ceph.com/issues/18371), [pr#13187](http://github.com/ceph/ceph/pull/13187), Kefu Chai)
- client: Fix lookup of "/.." in jewel ([issue#18408](http://tracker.ceph.com/issues/18408), [pr#12766](http://github.com/ceph/ceph/pull/12766), Jeff Layton)
- client: fix stale entries in command table ([issue#17974](http://tracker.ceph.com/issues/17974), [pr#12137](http://github.com/ceph/ceph/pull/12137), John Spray)
- client: populate metadata during mount ([issue#18361](http://tracker.ceph.com/issues/18361), [pr#13085](http://github.com/ceph/ceph/pull/13085), John Spray)
- cli: implement functionality for adding, editing and removing omap values with binary keys ([issue#18123](http://tracker.ceph.com/issues/18123), [pr#12755](http://github.com/ceph/ceph/pull/12755), Jason Dillaman)
- common: Improve linux dcache hash algorithm ([issue#17599](http://tracker.ceph.com/issues/17599), [pr#11529](http://github.com/ceph/ceph/pull/11529), Yibo Cai)
- common: utime.h: fix timezone issue in round\_to\_\* funcs. ([issue#14862](http://tracker.ceph.com/issues/14862), [pr#11508](http://github.com/ceph/ceph/pull/11508), Zhao Chao)
- doc: Python Swift client commands in Quick Developer Guide don't match configuration in vstart.sh ([issue#17746](http://tracker.ceph.com/issues/17746), [pr#13043](http://github.com/ceph/ceph/pull/13043), Ronak Jain)
- librbd: allow to open an image without opening parent image ([issue#18325](http://tracker.ceph.com/issues/18325), [pr#13130](http://github.com/ceph/ceph/pull/13130), Ricardo Dias)
- librbd: metadata\_set API operation should not change global config setting ([issue#18465](http://tracker.ceph.com/issues/18465), [pr#13168](http://github.com/ceph/ceph/pull/13168), Mykola Golub)
- librbd: new API method to force break a peer's exclusive lock ([issue#15632](http://tracker.ceph.com/issues/15632), [issue#16773](http://tracker.ceph.com/issues/16773), [issue#17188](http://tracker.ceph.com/issues/17188), [issue#16988](http://tracker.ceph.com/issues/16988), [issue#17210](http://tracker.ceph.com/issues/17210), [issue#17251](http://tracker.ceph.com/issues/17251), [issue#18429](http://tracker.ceph.com/issues/18429), [issue#17227](http://tracker.ceph.com/issues/17227), [issue#18327](http://tracker.ceph.com/issues/18327), [issue#17015](http://tracker.ceph.com/issues/17015), [pr#12890](http://github.com/ceph/ceph/pull/12890), Danny Al-Gaaf, Mykola Golub, Jason Dillaman)
- librbd: properly order concurrent updates to the object map ([issue#16176](http://tracker.ceph.com/issues/16176), [pr#12909](http://github.com/ceph/ceph/pull/12909), Jason Dillaman)
- librbd: restore journal access when force disabling mirroring ([issue#17588](http://tracker.ceph.com/issues/17588), [pr#11916](http://github.com/ceph/ceph/pull/11916), Mykola Golub)
- mds: Cannot create deep directories when caps contain path=/somepath ([issue#17858](http://tracker.ceph.com/issues/17858), [pr#12154](http://github.com/ceph/ceph/pull/12154), Patrick Donnelly)
- mds: cephfs metadata pool: deep-scrub error omap\_digest != best guess omap\_digest ([issue#17177](http://tracker.ceph.com/issues/17177), [pr#12380](http://github.com/ceph/ceph/pull/12380), Yan, Zheng)
- mds: cephfs test failures (ceph.com/qa is broken, should be download.ceph.com/qa) ([issue#18574](http://tracker.ceph.com/issues/18574), [pr#13023](http://github.com/ceph/ceph/pull/13023), John Spray)
- mds: ceph-fuse crash during snapshot tests ([issue#18460](http://tracker.ceph.com/issues/18460), [pr#13120](http://github.com/ceph/ceph/pull/13120), Yan, Zheng)
- mds: ceph\_volume\_client: fix recovery from partial auth update ([issue#17216](http://tracker.ceph.com/issues/17216), [pr#11656](http://github.com/ceph/ceph/pull/11656), Ramana Raja)
- mds: ceph\_volume\_client.py : Error: Can't handle arrays of non-strings ([issue#17800](http://tracker.ceph.com/issues/17800), [pr#12325](http://github.com/ceph/ceph/pull/12325), Ramana Raja)
- mds: Cleanly reject session evict command when in replay ([issue#17801](http://tracker.ceph.com/issues/17801), [pr#12153](http://github.com/ceph/ceph/pull/12153), Yan, Zheng)
- mds: client segfault on ceph\_rmdir path / ([issue#9935](http://tracker.ceph.com/issues/9935), [pr#13029](http://github.com/ceph/ceph/pull/13029), Michal Jarzabek)
- mds: Clients without pool-changing caps shouldn't be allowed to change pool\_namespace ([issue#17798](http://tracker.ceph.com/issues/17798), [pr#12155](http://github.com/ceph/ceph/pull/12155), John Spray)
- mds: Decode errors on backtrace will crash MDS ([issue#18311](http://tracker.ceph.com/issues/18311), [pr#12836](http://github.com/ceph/ceph/pull/12836), Nathan Cutler, John Spray)
- mds: false failing to respond to cache pressure warning ([issue#17611](http://tracker.ceph.com/issues/17611), [pr#11861](http://github.com/ceph/ceph/pull/11861), Yan, Zheng)
- mds: finish clientreplay requests before requesting active state ([issue#18461](http://tracker.ceph.com/issues/18461), [pr#13113](http://github.com/ceph/ceph/pull/13113), Yan, Zheng)
- mds: fix incorrect assertion in Server::\_dir\_is\_nonempty() ([issue#18578](http://tracker.ceph.com/issues/18578), [pr#13459](http://github.com/ceph/ceph/pull/13459), Yan, Zheng)
- mds: fix MDSMap upgrade decoding ([issue#17837](http://tracker.ceph.com/issues/17837), [pr#13139](http://github.com/ceph/ceph/pull/13139), John Spray, Patrick Donnelly)
- mds: fix missing ll\_get for ll\_walk ([issue#18086](http://tracker.ceph.com/issues/18086), [pr#13125](http://github.com/ceph/ceph/pull/13125), Gui Hecheng)
- mds: Fix mount root for ceph\_mount users and change tarball format ([issue#18312](http://tracker.ceph.com/issues/18312), [issue#18254](http://tracker.ceph.com/issues/18254), [pr#12592](http://github.com/ceph/ceph/pull/12592), Jeff Layton)
- mds: fix null pointer dereference in Locker::handle\_client\_caps ([issue#18306](http://tracker.ceph.com/issues/18306), [pr#13060](http://github.com/ceph/ceph/pull/13060), Yan, Zheng)
- mds: lookup of /.. in returns -ENOENT ([issue#18408](http://tracker.ceph.com/issues/18408), [pr#12783](http://github.com/ceph/ceph/pull/12783), Jeff Layton)
- mds: MDS crashes on missing metadata object ([issue#18179](http://tracker.ceph.com/issues/18179), [pr#13119](http://github.com/ceph/ceph/pull/13119), Yan, Zheng)
- mds: mds fails to respawn if executable has changed ([issue#17531](http://tracker.ceph.com/issues/17531), [pr#11873](http://github.com/ceph/ceph/pull/11873), Patrick Donnelly)
- mds: MDS: false failing to respond to cache pressure warning ([issue#17716](http://tracker.ceph.com/issues/17716), [pr#11856](http://github.com/ceph/ceph/pull/11856), Yan, Zheng)
- mds: MDS goes damaged on blacklist (failed to read JournalPointer: -108 ((108) Cannot send after transport endpoint shutdown) ([issue#17236](http://tracker.ceph.com/issues/17236), [pr#11413](http://github.com/ceph/ceph/pull/11413), John Spray)
- mds: MDS long-time blocked ops. ceph-fuse locks up with getattr of file ([issue#17275](http://tracker.ceph.com/issues/17275), [pr#11858](http://github.com/ceph/ceph/pull/11858), Yan, Zheng)
- mds: speed up readdir by skipping unwanted dn ([issue#18519](http://tracker.ceph.com/issues/18519), [pr#12921](http://github.com/ceph/ceph/pull/12921), Xiaoxi Chen)
- mds: standby-replay daemons can sometimes miss events ([issue#17954](http://tracker.ceph.com/issues/17954), [pr#13126](http://github.com/ceph/ceph/pull/13126), John Spray)
- mon: cache tiering: base pool last\_force\_resend not respected (racing read got wrong version) ([issue#18366](http://tracker.ceph.com/issues/18366), [pr#13115](http://github.com/ceph/ceph/pull/13115), Sage Weil)
- mon: ceph osd down detection behaviour ([issue#18104](http://tracker.ceph.com/issues/18104), [pr#12677](http://github.com/ceph/ceph/pull/12677), xie xingguo)
- mon: Error EINVAL: removing mon.a at 172.21.15.16:6789/0, there will be 1 monitors ([issue#17725](http://tracker.ceph.com/issues/17725), [pr#11999](http://github.com/ceph/ceph/pull/11999), Joao Eduardo Luis)
- mon: health does not report pgs stuck in more than one state ([issue#17515](http://tracker.ceph.com/issues/17515), [pr#11660](http://github.com/ceph/ceph/pull/11660), Sage Weil)
- mon: monitor assertion failure when deactivating mds in (invalid) fscid 0 ([issue#17518](http://tracker.ceph.com/issues/17518), [pr#11862](http://github.com/ceph/ceph/pull/11862), Patrick Donnelly)
- mon: monitor cannot start because of FAILED assert(info.state == MDSMap::STATE\_STANDBY) ([issue#18166](http://tracker.ceph.com/issues/18166), [pr#13123](http://github.com/ceph/ceph/pull/13123), John Spray, Patrick Donnelly)
- mon: osd flag health message is misleading ([issue#18175](http://tracker.ceph.com/issues/18175), [pr#13117](http://github.com/ceph/ceph/pull/13117), Sage Weil)
- mon: OSDMonitor: clear jewel+ feature bits when talking to Hammer OSD ([issue#18582](http://tracker.ceph.com/issues/18582), [pr#13131](http://github.com/ceph/ceph/pull/13131), Piotr Dałek)
- mon: OSDs marked OUT wrongly after monitor failover ([issue#17719](http://tracker.ceph.com/issues/17719), [pr#11947](http://github.com/ceph/ceph/pull/11947), Dong Wu)
- mon: peon wrongly delete routed pg stats op before receive pg stats ack ([issue#18458](http://tracker.ceph.com/issues/18458), [pr#13045](http://github.com/ceph/ceph/pull/13045), Mingxin Liu)
- mon: send updated monmap to its subscribers ([issue#17558](http://tracker.ceph.com/issues/17558), [pr#11743](http://github.com/ceph/ceph/pull/11743), Kefu Chai)
- msgr: don't truncate message sequence to 32-bits ([issue#16122](http://tracker.ceph.com/issues/16122), [pr#12416](http://github.com/ceph/ceph/pull/12416), Yan, Zheng)
- msgr: msg/simple: clear\_pipe when wait() is mopping up pipes ([issue#15784](http://tracker.ceph.com/issues/15784), [pr#13062](http://github.com/ceph/ceph/pull/13062), Sage Weil)
- msgr: msg/simple/Pipe: error decoding addr ([issue#18072](http://tracker.ceph.com/issues/18072), [pr#12291](http://github.com/ceph/ceph/pull/12291), Sage Weil)
- osd: Add config option to disable new scrubs during recovery ([issue#17866](http://tracker.ceph.com/issues/17866), [pr#11944](http://github.com/ceph/ceph/pull/11944), Wido den Hollander)
- osd: collection\_list shadow return value # ([issue#17713](http://tracker.ceph.com/issues/17713), [pr#11737](http://github.com/ceph/ceph/pull/11737), Haomai Wang)
- osd: do not send ENXIO on misdirected op by default ([issue#18751](http://tracker.ceph.com/issues/18751), [pr#13255](http://github.com/ceph/ceph/pull/13255), Sage Weil)
- osd: FileStore: fiemap cannot be totally retrieved in xfs when the number of extents > 1364 ([issue#17610](http://tracker.ceph.com/issues/17610), [pr#11998](http://github.com/ceph/ceph/pull/11998), Kefu Chai, Ning Yao)
- osd: leveldb corruption leads to Operation not permitted not handled and assert ([issue#18037](http://tracker.ceph.com/issues/18037), [pr#12789](http://github.com/ceph/ceph/pull/12789), Nathan Cutler)
- osd: limit omap data in push op ([issue#16128](http://tracker.ceph.com/issues/16128), [pr#11991](http://github.com/ceph/ceph/pull/11991), Wanlong Gao)
- osd: osd crashes when radosgw-admin bi list --max-entries=1 command runing ([issue#17745](http://tracker.ceph.com/issues/17745), [pr#11758](http://github.com/ceph/ceph/pull/11758), weiqiaomiao)
- osd: osd\_max\_backfills default has changed, documentation should reflect that. ([issue#17701](http://tracker.ceph.com/issues/17701), [pr#11735](http://github.com/ceph/ceph/pull/11735), huangjun)
- osd: OSDMonitor: only reject MOSDBoot based on up\_from if inst matches ([issue#17899](http://tracker.ceph.com/issues/17899), [pr#12868](http://github.com/ceph/ceph/pull/12868), Samuel Just)
- osd: osd/PG: publish PG stats when backfill-related states change ([issue#18369](http://tracker.ceph.com/issues/18369), [pr#12875](http://github.com/ceph/ceph/pull/12875), Alexey Sheplyakov, Sage Weil)
- osd: Remove extra call to reg\_next\_scrub() during splits ([issue#16474](http://tracker.ceph.com/issues/16474), [pr#11606](http://github.com/ceph/ceph/pull/11606), David Zafman)
- osd: Revert "Merge pull request #12978 from asheplyakov/jewel-18581" ([issue#18809](http://tracker.ceph.com/issues/18809), [pr#13280](http://github.com/ceph/ceph/pull/13280), Samuel Just)
- osd: update\_log\_missing does not order correctly with osd\_ops ([issue#17789](http://tracker.ceph.com/issues/17789), [pr#11997](http://github.com/ceph/ceph/pull/11997), Samuel Just)
- qa/tasks: backport rbd\_fio fixes to jewel ([issue#13512](http://tracker.ceph.com/issues/13512), [pr#13104](http://github.com/ceph/ceph/pull/13104), Ilya Dryomov)
- qa/tasks/workunits: backport misc fixes to jewel ([issue#18336](http://tracker.ceph.com/issues/18336), [pr#12912](http://github.com/ceph/ceph/pull/12912), Sage Weil)
- rados: crash adding snap to purged\_snaps in ReplicatedPG::WaitingOnReplicas (part 2) ([issue#15943](http://tracker.ceph.com/issues/15943), [issue#18504](http://tracker.ceph.com/issues/18504), [pr#12791](http://github.com/ceph/ceph/pull/12791), Samuel Just)
- rados: Memory leaks in object\_list\_begin and object\_list\_end ([issue#18252](http://tracker.ceph.com/issues/18252), [pr#13118](http://github.com/ceph/ceph/pull/13118), Brad Hubbard)
- rados: The request lock RPC message might be incorrectly ignored ([issue#17030](http://tracker.ceph.com/issues/17030), [pr#10865](http://github.com/ceph/ceph/pull/10865), Jason Dillaman)
- rbd: add image id block name prefix APIs ([issue#18270](http://tracker.ceph.com/issues/18270), [pr#12529](http://github.com/ceph/ceph/pull/12529), Jason Dillaman)
- rbd: add max\_part and nbds\_max options in rbd nbd map, in order to keep consistent with ([issue#18186](http://tracker.ceph.com/issues/18186), [pr#12426](http://github.com/ceph/ceph/pull/12426), Pan Liu)
- rbd: Attempting to remove an image w/ incompatible features results in partial removal ([issue#18315](http://tracker.ceph.com/issues/18315), [pr#13156](http://github.com/ceph/ceph/pull/13156), Dongsheng Yang)
- rbd: bench-write will crash if --io-size is 4G ([issue#18422](http://tracker.ceph.com/issues/18422), [pr#13129](http://github.com/ceph/ceph/pull/13129), Gaurav Kumar Garg)
- rbd: diff calculate can hide parent extents when examining first snapshot in clone ([issue#18068](http://tracker.ceph.com/issues/18068), [pr#12322](http://github.com/ceph/ceph/pull/12322), Jason Dillaman)
- rbd: Exclusive lock improperly initialized on read-only image when using snap\_set API ([issue#17618](http://tracker.ceph.com/issues/17618), [pr#11852](http://github.com/ceph/ceph/pull/11852), Jason Dillaman)
- rbd: FAILED assert(m\_processing == 0) while running test\_lock\_fence.sh ([issue#17973](http://tracker.ceph.com/issues/17973), [pr#12323](http://github.com/ceph/ceph/pull/12323), Venky Shankar)
- rbd: Improve error reporting from rbd feature enable/disable ([issue#16985](http://tracker.ceph.com/issues/16985), [pr#13157](http://github.com/ceph/ceph/pull/13157), Gaurav Kumar Garg)
- rbd: JournalMetadata flooding with errors when being blacklisted ([issue#18243](http://tracker.ceph.com/issues/18243), [pr#12739](http://github.com/ceph/ceph/pull/12739), Jason Dillaman)
- rbd: librbd: use proper snapshot when computing diff parent overlap ([issue#18200](http://tracker.ceph.com/issues/18200), [pr#12649](http://github.com/ceph/ceph/pull/12649), Xiaoxi Chen)
- rbd: partition func should be enabled When load nbd.ko for rbd-nbd ([issue#18115](http://tracker.ceph.com/issues/18115), [pr#12754](http://github.com/ceph/ceph/pull/12754), Pan Liu)
- rbd: Potential race when removing two-way mirroring image ([issue#18447](http://tracker.ceph.com/issues/18447), [pr#13233](http://github.com/ceph/ceph/pull/13233), Mykola Golub)
- rbd: \[qa\] crash in journal-enabled fsx run ([issue#18618](http://tracker.ceph.com/issues/18618), [pr#13128](http://github.com/ceph/ceph/pull/13128), Jason Dillaman)
- rbd: 'rbd du' of missing image does not return error ([issue#16987](http://tracker.ceph.com/issues/16987), [pr#11854](http://github.com/ceph/ceph/pull/11854), Dongsheng Yang)
- rbd: rbd-mirror: gmock warnings in bootstrap request unit tests ([issue#18048](http://tracker.ceph.com/issues/18048), [issue#18012](http://tracker.ceph.com/issues/18012), [issue#18156](http://tracker.ceph.com/issues/18156), [issue#16991](http://tracker.ceph.com/issues/16991), [issue#18051](http://tracker.ceph.com/issues/18051), [pr#12425](http://github.com/ceph/ceph/pull/12425), Mykola Golub)
- rbd: rbd-mirror: image sync object map reload logs message ([issue#16179](http://tracker.ceph.com/issues/16179), [pr#12753](http://github.com/ceph/ceph/pull/12753), runsisi)
- rbd: rbd-mirror: snap protect of non-layered image results in split-brain ([issue#16962](http://tracker.ceph.com/issues/16962), [pr#11869](http://github.com/ceph/ceph/pull/11869), Mykola Golub)
- rbd: \[rbd-mirror\] sporadic image replayer shut down failure ([issue#18441](http://tracker.ceph.com/issues/18441), [pr#13155](http://github.com/ceph/ceph/pull/13155), Jason Dillaman)
- rbd: rbd-nbd: disallow mapping images >2TB in size ([issue#17219](http://tracker.ceph.com/issues/17219), [pr#11870](http://github.com/ceph/ceph/pull/11870), Mykola Golub)
- rbd: rbd-nbd: invalid error code for "failed to read nbd request" messages ([issue#18242](http://tracker.ceph.com/issues/18242), [pr#12756](http://github.com/ceph/ceph/pull/12756), Mykola Golub)
- rbd: status json format has duplicated/overwritten key ([issue#18261](http://tracker.ceph.com/issues/18261), [pr#12741](http://github.com/ceph/ceph/pull/12741), Mykola Golub)
- rbd: TestLibRBD.DiscardAfterWrite doesn't handle rbd\_skip\_partial\_discard = true ([issue#17750](http://tracker.ceph.com/issues/17750), [pr#11853](http://github.com/ceph/ceph/pull/11853), Jason Dillaman)
- rbd: truncate can cause unflushed snapshot data lose ([issue#17193](http://tracker.ceph.com/issues/17193), [pr#12324](http://github.com/ceph/ceph/pull/12324), Yan, Zheng)
- : ReplicatedBackend: take read locks for clone sources during recovery ([issue#17831](http://tracker.ceph.com/issues/17831), [issue#18583](http://tracker.ceph.com/issues/18583), [pr#12978](http://github.com/ceph/ceph/pull/12978), Samuel Just)
- rgw: add option to log custom HTTP headers (rgw\_log\_http\_headers) ([issue#18891](http://tracker.ceph.com/issues/18891), [pr#12490](http://github.com/ceph/ceph/pull/12490), Matt Benjamin)
- rgw: add suport for Swift-at-root dependent features of Swift API ([issue#18526](http://tracker.ceph.com/issues/18526), [issue#16673](http://tracker.ceph.com/issues/16673), [pr#11497](http://github.com/ceph/ceph/pull/11497), Pritha Srivastava, Radoslaw Zarzynski, Pete Zaitcev, Abhishek Lekshmanan)
- rgw: add support for the prefix parameter in account listing of Swift API ([issue#17931](http://tracker.ceph.com/issues/17931), [pr#12258](http://github.com/ceph/ceph/pull/12258), Radoslaw Zarzynski)
- rgw: Add workaround for upgrade issues for older jewel versions ([issue#17820](http://tracker.ceph.com/issues/17820), [pr#12316](http://github.com/ceph/ceph/pull/12316), Orit Wasserman)
- rgw: be aware abount tenants on cls\_user\_bucket -> rgw\_bucket conversion ([issue#18364](http://tracker.ceph.com/issues/18364), [issue#16355](http://tracker.ceph.com/issues/16355), [pr#13276](http://github.com/ceph/ceph/pull/13276), Radoslaw Zarzynski)
- rgw: bucket check remove \_multipart\_ prefix ([issue#13724](http://tracker.ceph.com/issues/13724), [pr#11470](http://github.com/ceph/ceph/pull/11470), Weijun Duan)
- rgw: bucket resharding ([issue#17549](http://tracker.ceph.com/issues/17549), [issue#17550](http://tracker.ceph.com/issues/17550), [pr#13341](http://github.com/ceph/ceph/pull/13341), Yehuda Sadeh, Robin H. Johnson)
- rgw: disable virtual hosting of buckets when no hostnames are configured ([issue#17440](http://tracker.ceph.com/issues/17440), [issue#15975](http://tracker.ceph.com/issues/15975), [issue#17136](http://tracker.ceph.com/issues/17136), [pr#11760](http://github.com/ceph/ceph/pull/11760), Casey Bodley, Robin H. Johnson)
- rgw: do not abort when accept a CORS request with short origin ([issue#18187](http://tracker.ceph.com/issues/18187), [pr#12397](http://github.com/ceph/ceph/pull/12397), LiuYang)
- rgw: don't store empty chains in gc ([issue#17897](http://tracker.ceph.com/issues/17897), [pr#12174](http://github.com/ceph/ceph/pull/12174), Yehuda Sadeh)
- rgw:fix for deleting objects name beginning and ending with underscores of one bucket using POST method of js sdk. ([issue#17888](http://tracker.ceph.com/issues/17888), [pr#12320](http://github.com/ceph/ceph/pull/12320), Casey Bodley)
- rgw: fix period update crash ([issue#18631](http://tracker.ceph.com/issues/18631), [pr#13273](http://github.com/ceph/ceph/pull/13273), Orit Wasserman)
- rgw: fix put\_acls for objects starting and ending with underscore ([issue#17625](http://tracker.ceph.com/issues/17625), [pr#11675](http://github.com/ceph/ceph/pull/11675), Orit Wasserman)
- rgw: fix use of marker in List::list\_objects() ([issue#18331](http://tracker.ceph.com/issues/18331), [pr#13358](http://github.com/ceph/ceph/pull/13358), Yehuda Sadeh)
- rgw: for the create\_bucket api, if the input creation\_time is zero, we … ([issue#16597](http://tracker.ceph.com/issues/16597), [pr#11990](http://github.com/ceph/ceph/pull/11990), weiqiaomiao)
- rgw: Have a flavor of bucket deletion in radosgw-admin to bypass garbage collection ([issue#15557](http://tracker.ceph.com/issues/15557), [pr#10661](http://github.com/ceph/ceph/pull/10661), Pavan Rallabhandi)
- rgw: json encode/decode of RGWBucketInfo missing index\_type field ([issue#17755](http://tracker.ceph.com/issues/17755), [pr#11759](http://github.com/ceph/ceph/pull/11759), Yehuda Sadeh)
- rgw: ldap: enforce simple\_bind w/LDAPv3 redux ([issue#18339](http://tracker.ceph.com/issues/18339), [pr#12678](http://github.com/ceph/ceph/pull/12678), Weibing Zhang)
- rgw: leak from RGWMetaSyncShardCR::incremental\_sync ([issue#18412](http://tracker.ceph.com/issues/18412), [issue#18300](http://tracker.ceph.com/issues/18300), [pr#13004](http://github.com/ceph/ceph/pull/13004), Casey Bodley, Sage Weil)
- rgw: leak in RGWFetchAllMetaCR ([issue#17812](http://tracker.ceph.com/issues/17812), [pr#11872](http://github.com/ceph/ceph/pull/11872), Casey Bodley)
- rgw: librgw: objects created from s3 apis are not visible from nfs mount point ([issue#18651](http://tracker.ceph.com/issues/18651), [pr#13177](http://github.com/ceph/ceph/pull/13177), Matt Benjamin)
- rgw: log name instead of id for SystemMetaObj on failure ([issue#15776](http://tracker.ceph.com/issues/15776), [pr#12622](http://github.com/ceph/ceph/pull/12622), Wido den Hollander, Abhishek Lekshmanan)
- rgw: multimds: mds entering up:replay and processing down mds aborts ([issue#17670](http://tracker.ceph.com/issues/17670), [pr#11857](http://github.com/ceph/ceph/pull/11857), Patrick Donnelly)
- rgw: multipart upload copy ([issue#12790](http://tracker.ceph.com/issues/12790), [pr#13068](http://github.com/ceph/ceph/pull/13068), Yehuda Sadeh, Javier M. Mellid, Matt Benjamin)
- rgw: multisite: after finishing full sync on a bucket, incremental sync starts over from the beginning ([issue#17661](http://tracker.ceph.com/issues/17661), [issue#17624](http://tracker.ceph.com/issues/17624), [pr#11864](http://github.com/ceph/ceph/pull/11864), Zengran Zhang, Casey Bodley)
- rgw: multisite: assert(next) failed in RGWMetaSyncCR ([issue#17044](http://tracker.ceph.com/issues/17044), [pr#11477](http://github.com/ceph/ceph/pull/11477), Casey Bodley)
- rgw: multisite: coroutine deadlock assertion on error in FetchAllMetaCR ([issue#17571](http://tracker.ceph.com/issues/17571), [pr#11866](http://github.com/ceph/ceph/pull/11866), Casey Bodley)
- rgw: multisite: coroutine deadlock in RGWMetaSyncCR after ECANCELED errors ([issue#17465](http://tracker.ceph.com/issues/17465), [pr#12738](http://github.com/ceph/ceph/pull/12738), Casey Bodley)
- rgw: multisite doesn't retry RGWFetchAllMetaCR on failed lease ([issue#17047](http://tracker.ceph.com/issues/17047), [pr#11476](http://github.com/ceph/ceph/pull/11476), Casey Bodley)
- rgw: multisite: ECANCELED & 500 error on bucket delete ([issue#17698](http://tracker.ceph.com/issues/17698), [pr#12044](http://github.com/ceph/ceph/pull/12044), Casey Bodley)
- rgw: multisite: failed assertion in 'radosgw-admin bucket sync status' ([issue#18083](http://tracker.ceph.com/issues/18083), [pr#12314](http://github.com/ceph/ceph/pull/12314), Casey Bodley)
- rgw: multisite: fix ref counting of completions ([issue#17792](http://tracker.ceph.com/issues/17792), [issue#18414](http://tracker.ceph.com/issues/18414), [issue#17793](http://tracker.ceph.com/issues/17793), [issue#18407](http://tracker.ceph.com/issues/18407), [pr#13001](http://github.com/ceph/ceph/pull/13001), Casey Bodley)
- rgw: multisite: metadata master can get the wrong value for 'oldest\_log\_period' ([issue#16894](http://tracker.ceph.com/issues/16894), [pr#11868](http://github.com/ceph/ceph/pull/11868), Casey Bodley)
- rgw: multisite: obsolete 'radosgw-admin period prepare' command ([issue#17387](http://tracker.ceph.com/issues/17387), [pr#11574](http://github.com/ceph/ceph/pull/11574), Gaurav Kumar Garg)
- rgw: multisite: race between ReadSyncStatus and InitSyncStatus leads to EIO errors ([issue#17568](http://tracker.ceph.com/issues/17568), [pr#11865](http://github.com/ceph/ceph/pull/11865), Casey Bodley)
- rgw: multisite requests failing with '400 Bad Request' with civetweb 1.8 ([issue#17822](http://tracker.ceph.com/issues/17822), [pr#12313](http://github.com/ceph/ceph/pull/12313), Casey Bodley)
- rgw: multisite: segfault after changing value of rgw\_data\_log\_num\_shards ([issue#18488](http://tracker.ceph.com/issues/18488), [pr#13180](http://github.com/ceph/ceph/pull/13180), Casey Bodley)
- rgw: multisite: sync status reports master is on a different period ([issue#18064](http://tracker.ceph.com/issues/18064), [pr#13175](http://github.com/ceph/ceph/pull/13175), Abhishek Lekshmanan)
- rgw: multisite upgrade from hammer -> jewel ignores rgw\_region\_root\_pool ([issue#17963](http://tracker.ceph.com/issues/17963), [pr#12156](http://github.com/ceph/ceph/pull/12156), Casey Bodley)
- rgw: radosgw-admin period update reverts deleted zonegroup ([issue#17239](http://tracker.ceph.com/issues/17239), [pr#13171](http://github.com/ceph/ceph/pull/13171), Orit Wasserman)
- rgw: Realm set does not create a new period ([issue#18333](http://tracker.ceph.com/issues/18333), [pr#13182](http://github.com/ceph/ceph/pull/13182), Orit Wasserman)
- rgw: remove spurious mount entries for RGW buckets ([issue#17850](http://tracker.ceph.com/issues/17850), [pr#12045](http://github.com/ceph/ceph/pull/12045), Matt Benjamin)
- rgw: Replacing '+' with "%20" in canonical uri for s3 v4 auth. ([issue#17076](http://tracker.ceph.com/issues/17076), [pr#12542](http://github.com/ceph/ceph/pull/12542), Pritha Srivastava)
- rgw: rgw-admin: missing command to modify placement targets ([issue#18078](http://tracker.ceph.com/issues/18078), [pr#12428](http://github.com/ceph/ceph/pull/12428), Yehuda Sadeh, Casey Bodley)
- rgw: RGWRados::get\_system\_obj() sends unnecessary stat request before read ([issue#17580](http://tracker.ceph.com/issues/17580), [pr#11867](http://github.com/ceph/ceph/pull/11867), Casey Bodley)
- rgw: rgw\_rest\_s3: apply missed base64 try-catch ([issue#17663](http://tracker.ceph.com/issues/17663), [pr#11672](http://github.com/ceph/ceph/pull/11672), Matt Benjamin)
- rgw: RGW will not list Argonaut-era bucket via HTTP (but radosgw-admin works) ([issue#17372](http://tracker.ceph.com/issues/17372), [pr#11863](http://github.com/ceph/ceph/pull/11863), Yehuda Sadeh)
- rgw: sends omap\_getvals with (u64)-1 limit ([issue#17985](http://tracker.ceph.com/issues/17985), [pr#12419](http://github.com/ceph/ceph/pull/12419), Yehuda Sadeh, Sage Weil)
- rgw: slave zonegroup cannot enable the bucket versioning ([issue#18003](http://tracker.ceph.com/issues/18003), [pr#13173](http://github.com/ceph/ceph/pull/13173), Orit Wasserman)
- rgw: TempURL properly handles accounts created with the implicit tenant ([issue#17961](http://tracker.ceph.com/issues/17961), [pr#12079](http://github.com/ceph/ceph/pull/12079), Radoslaw Zarzynski)
- rgw: the value of total\_time is wrong in the result of 'radosgw-admin log show' opt ([issue#17598](http://tracker.ceph.com/issues/17598), [pr#11876](http://github.com/ceph/ceph/pull/11876), weiqiaomiao)
- rgw: Unable to commit period zonegroup change ([issue#17364](http://tracker.ceph.com/issues/17364), [pr#12315](http://github.com/ceph/ceph/pull/12315), Orit Wasserman)
- rgw: valgrind "invalid read size 4" RGWGetObj ([issue#18071](http://tracker.ceph.com/issues/18071), [pr#12997](http://github.com/ceph/ceph/pull/12997), Matt Benjamin)
- rgw: work around curl\_multi\_wait bug with non-blocking reads ([issue#15915](http://tracker.ceph.com/issues/15915), [issue#16368](http://tracker.ceph.com/issues/16368), [issue#16695](http://tracker.ceph.com/issues/16695), [pr#11627](http://github.com/ceph/ceph/pull/11627), John Coyle, Casey Bodley)
- tests: add require\_jewel\_osds before upgrading last hammer node ([issue#18719](http://tracker.ceph.com/issues/18719), [pr#13161](http://github.com/ceph/ceph/pull/13161), Nathan Cutler)
- tests: add require\_jewel\_osds to upgrade/hammer-x/tiering ([issue#18920](http://tracker.ceph.com/issues/18920), [pr#13404](http://github.com/ceph/ceph/pull/13404), Nathan Cutler)
- tests: assertion failure in a radosgw-admin related task ([issue#17167](http://tracker.ceph.com/issues/17167), [pr#12764](http://github.com/ceph/ceph/pull/12764), Orit Wasserman)
- tests: Cannot reserve CentOS 7.2 smithi machines ([issue#18416](http://tracker.ceph.com/issues/18416), [issue#18401](http://tracker.ceph.com/issues/18401), [pr#13050](http://github.com/ceph/ceph/pull/13050), Nathan Cutler, Sage Weil, Yuri Weinstein)
- tests: ignore bogus ceph-objectstore-tool error in ceph\_manager ([issue#16263](http://tracker.ceph.com/issues/16263), [pr#13240](http://github.com/ceph/ceph/pull/13240), Nathan Cutler, Kefu Chai)
- tests: objecter\_requests workunit fails on wip branches ([issue#18393](http://tracker.ceph.com/issues/18393), [pr#12761](http://github.com/ceph/ceph/pull/12761), Sage Weil)
- tests: qa/suites/upgrade/hammer-x: break stress split ec symlinks ([issue#19006](http://tracker.ceph.com/issues/19006), [pr#13533](http://github.com/ceph/ceph/pull/13533), Nathan Cutler)
- tests: qa/suites/upgrade/hammer-x/stress-split: finish thrashing before final upgrade ([issue#19004](http://tracker.ceph.com/issues/19004), [pr#13222](http://github.com/ceph/ceph/pull/13222), Sage Weil)
- tests: qa/tasks/ceph\_deploy.py: use dev option ([issue#18736](http://tracker.ceph.com/issues/18736), [pr#13106](http://github.com/ceph/ceph/pull/13106), Vasu Kulkarni)
- tests: qa/workunits/rbd: use more recent qemu-iotests that support Xenial ([issue#18149](http://tracker.ceph.com/issues/18149), [issue#10773](http://tracker.ceph.com/issues/10773), [pr#13103](http://github.com/ceph/ceph/pull/13103), Jason Dillaman)
- tests: remove qa/suites/buildpackages ([issue#18846](http://tracker.ceph.com/issues/18846), [pr#13299](http://github.com/ceph/ceph/pull/13299), Loic Dachary)
- tests: SUSE yaml facets in qa/distros/all are out of date ([issue#18856](http://tracker.ceph.com/issues/18856), [issue#18846](http://tracker.ceph.com/issues/18846), [pr#13331](http://github.com/ceph/ceph/pull/13331), Nathan Cutler)
- tests: update rbd/singleton/all/formatted-output.yaml to support ceph-ci ([issue#18440](http://tracker.ceph.com/issues/18440), [pr#12822](http://github.com/ceph/ceph/pull/12822), Nathan Cutler, Venky Shankar)
- tests: update Ubuntu image url after ceph.com refactor ([issue#18542](http://tracker.ceph.com/issues/18542), [pr#12959](http://github.com/ceph/ceph/pull/12959), Jason Dillaman)
- tests: upgrade:hammer-x: install firefly only on Ubuntu 14.04 ([issue#18089](http://tracker.ceph.com/issues/18089), [pr#13153](http://github.com/ceph/ceph/pull/13153), Nathan Cutler)
- tests: use ceph-jewel branch for s3tests ([issue#18384](http://tracker.ceph.com/issues/18384), [pr#12745](http://github.com/ceph/ceph/pull/12745), Nathan Cutler)
- tests: Workunits needlessly wget from git.ceph.com ([issue#18336](http://tracker.ceph.com/issues/18336), [issue#18271](http://tracker.ceph.com/issues/18271), [issue#18388](http://tracker.ceph.com/issues/18388), [pr#12686](http://github.com/ceph/ceph/pull/12686), Nathan Cutler, Sage Weil)
- test: temporarily disable fork()'ing tests ([issue#16556](http://tracker.ceph.com/issues/16556), [issue#17832](http://tracker.ceph.com/issues/17832), [pr#11953](http://github.com/ceph/ceph/pull/11953), John Spray)
- test: test fails due to The UNIX domain socket path ([issue#16014](http://tracker.ceph.com/issues/16014), [pr#12151](http://github.com/ceph/ceph/pull/12151), Loic Dachary)
- tools: ceph-disk: ceph-disk@.service races with ceph-osd@.service ([issue#17889](http://tracker.ceph.com/issues/17889), [issue#17813](http://tracker.ceph.com/issues/17813), [pr#12147](http://github.com/ceph/ceph/pull/12147), Loic Dachary)
- tools: ceph-disk --dmcrypt create must not require admin key ([issue#17849](http://tracker.ceph.com/issues/17849), [pr#12033](http://github.com/ceph/ceph/pull/12033), Loic Dachary)
- tools: ceph-disk prepare writes osd log 0 with root owner ([issue#18538](http://tracker.ceph.com/issues/18538), [pr#13025](http://github.com/ceph/ceph/pull/13025), Samuel Matzek)
- tools: crushtool --compile is create output despite of missing item ([issue#17306](http://tracker.ceph.com/issues/17306), [pr#11410](http://github.com/ceph/ceph/pull/11410), Kefu Chai)
- tools: rados bench seq must verify the hostname ([issue#17526](http://tracker.ceph.com/issues/17526), [pr#13049](http://github.com/ceph/ceph/pull/13049), Loic Dachary)
- tools: snapshotted RBD extent objects can't be manually evicted from a cache tier ([issue#17896](http://tracker.ceph.com/issues/17896), [pr#11968](http://github.com/ceph/ceph/pull/11968), Mingxin Liu)
- tools: systemd/ceph-disk: reduce ceph-disk flock contention ([issue#18049](http://tracker.ceph.com/issues/18049), [issue#13160](http://tracker.ceph.com/issues/13160), [pr#12210](http://github.com/ceph/ceph/pull/12210), David Disseldorp)
