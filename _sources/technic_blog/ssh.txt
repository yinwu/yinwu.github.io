SSH
===

introduction
------------

libssh can run on top of either **libgcrypt** or **libcrypto**, two general-purpose cryptographic libraries


The sftp and scp subsystems use channels,

but libssh hides them to the programmer. If you want to use those subsystems, instead of a channel, you'll usually open a "sftp session" or a "scp session".

