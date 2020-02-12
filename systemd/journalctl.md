systemd journalctl
---


journalctl can read journal files from STDIN.


#### src/journal/journalctl.c
```c
         case ARG_FILE:
			if (streq(optarg, "-"))
                    /* An undocumented feature: we can read journal files from STDIN. We don't document
                     * this though, since after all we only support this for mmap-able, seekable files, and
                     * not for example pipes which are probably the primary usecase for reading things from
	                 * STDIN. To avoid confusion we hence don't document this feature. */
                     arg_file_stdin = true;
                     else {
                            r = glob_extend(&arg_file, optarg);
                            if (r < 0)
                                 return log_error_errno(r, "Failed to add paths: %m");
                     }
                     break;
```
