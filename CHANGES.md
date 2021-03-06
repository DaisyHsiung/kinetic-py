Changes since 0.8.2
===========================
>**NOTE:** this section will document changes to the library since the last release

## Important
- Kinetic Protocol version updated to [3.0.6](https://github.com/Seagate/kinetic-protocol/tree/3.0.6)
- Deprecrated classes and methods will be removed on the next major release.

## New features
- Added support for Batch operations
- Added `reverse` parameter on GetKeyRange operation 

## Major changes
- `AsyncClient` has been renamed to `Client`
- A new `SecureClient` has been added to `kinetic`.

## Minor changes
- Added env variable _KINETIC_CONNECT_TIMEOUT_ to control default connection timeout.

## Deprecated features
- Old blocking `Client` has been moved to `kinetic.depracated.BlockingClient`
- Old `AdminClient` has been moved to `kinetic.depracated.AdminClient`

## Misc
- Added alias for `AsyncClient = Client` to smooth transition.
- Added alias on `kinetic` for `AdminClient` to smooth transition.

Changes from 0.8.1 to 0.8.2
===========================

## Bug fixes
- Keys with empty values show correctly as '' instead of None
- **WRITEBACK** set as default mode for `put` and `delete` operations

## Misc
- OSX requirements for SSL connections updated.

Changes from 0.8.0 to 0.8.1
===========================
This section will document changes to the library since the last release

## Important
- Kinetic Protocol version updated to [3.0.5](https://github.com/Seagate/kinetic-protocol/tree/3.0.5)

## New features
- Added timeout, time_quanta, priority and early_exit support
- Pin size added to limits
- SHA1 calculation used as default on puts when algorithm and tag not specified.

## Minor changes
- The client will use WRITEBACK as default when synchronization mode not specified on PUT and DELETE.

Changes from 0.7.3 to 0.8.0
===========================

## Important
- Kinetic Protocol version updated to [3.0.0](https://github.com/Seagate/kinetic-protocol/tree/3.0.0)
- Everything requires proto 3.0.0 or higher on the device
- Devices pre 3.0.0 do not have handshakes and will raise Handshake timeout

## New features
- Added `--version` to cmd line tool
- Added background operations Scan and Optimize
- Added pin operations (Lock, unlock, erase, secureErase)
- Client auto configures cluster_version based on initial handshake
- ErasePin and LockPin can be set during the security operation
- Client fields config and limits show device information
- Added unsolicited status support
- Pin based operations MUST have a pin set and SSL enabled
- setSecurity MUST have SSL enabled
- getLog / getLogAsync added to Client/AsyncClient

## Behavior changes
- Removed GreenClient (Feature overlap with AsyncClient)
- Removed PipelinedClient (Only used internally by the kineticc)
- setPin removed from AdminClient

Changes from 0.7.2 to 0.7.3
===========================

## Important
- Kinetic Protocol version updated to [2.0.6](https://github.com/Seagate/kinetic-protocol/tree/2.0.6)

## New features
- Added handshake to negotiate connection id during connect
- Added TCP_NODELAY socket option to improve performance
- GetKeyRange operations now accept None arguments on keys (Issue #10)

## Behavior changes
- Removed DEVICE log from LogTypes.add() (Issue #15)

## Bug Fixes
- Fixed problem with status validation on the AdminClient
- Fixed error message when Magic number is invalid

Changes from 0.7.1 to 0.7.2
===========================

## Important
- Kinetic Protocol version updated to [2.0.5](https://github.com/Seagate/kinetic-protocol/tree/2.0.5)
- The compiled python proto kinetic/kinetic_pb2.py is now included on the repo

## New features
- Added zero copy support on puts and gets (Requires splice system call)
- Added IPv6 address support on all clients (Issue #8)
- Added new exception type ClusterVersionFailureException (Requires drive version 2.0.4)
- Added new Device specific GetLog (Requires protocol 2.0.5)
- Added SSL/TLS support on all clients

## Bug Fixes
- Fixed bug on invalid magix number (PR #11 contributed by @rpcope1, ASOKVAD-313)
- Fixex bug that caused close() and connect() to fail on a connection that faulted (Issue #7)
- Fixed a bug that caused the AsyncClient to crash when calling close()

Changes from 0.7.0 to 0.7.1
===========================

## New features
- Added setSecurity on AdminClient
- Added getVersion and getVersionAsync to the library.

## Bug Fixes
- Fixed tests not running and testcases with hardcoded 'localhost'
- Fixed flush operation build parameters (Merge #5, contributed by @rpcope1).
- AsyncClient returns NotConnected exception when an operation is attempted on a client before calling connect().
- Lowered default number of keys asked on ranges to 200 (ASKOVAD-287).
- Fixed typo on baset test case (Merge #2, contributed by @zaitcev).

Changes from 0.6.0.2 to 0.7.0
=============================

## Important
Kinetic Protocol version updated to 2.0.3

## New features
- Added Flush command (Requires protocol 2.0.3).
- Added Limits section on GetLog (Requires protocol 2.0.3).
- Added protocol_version field on kinetic module.
- Added version field on kinetic module.

## Breaking changes
- Renamed Synchronization.ASYNC to Synchronization.WRITEBACK
- Renamed Synchronization.SYNC to Synchronization.WRITETHROUGH

## Bug Fixes
- Fixed issue with asynchronous clients leaving the socket open after _close_ was called (ASOKVAD-263).
