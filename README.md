# cli_diff
argparse I used to handle command line arguments.
Asyncio is used to runtime_diff commands_line concurrently
== Arista switch show interface, inventory and bgp
interfaces and inventory can start at the same time.
bgp_summary must wait until interfaces finishes.
=================

I used Codespaces 

Created an example txt file/task
cat <<EOF > commands_line.txt
interfaces, 2, []
bgp_summary, 3, [interfaces]
inventory, 1, []
EOF

Run 
@z-github2030 ➜ /workspaces/cli_diff (main) $ cat <<EOF > commands_line.txt
interfaces, 2, []
bgp_summary, 3, [interfaces]
inventory, 1, []
EOF

@z-github2030 ➜ /workspaces/cli_diff (main) $ ls
README.md  commands_line.txt  v1
@z-github2030 ➜ /workspaces/cli_diff (main) $ python3 v1 commands_line.txt 
@z-github2030 ➜ /workspaces/cli_diff (main) $ ^C
@z-github2030 ➜ /workspaces/cli_diff (main) $ python3 v1 --validate_input_output commands_line.txt
Expected runtime_difftime = 5 sec
@z-github2030 ➜ /workspaces/cli_diff (main) $ 
@z-github2030 ➜ /workspaces/cli_diff (main) $ python3 v1 --runtime-diff commands_line.txt 
usage: v1 [-h] [--validate_input_output] [--runtime_diff] file
v1: error: unrecognized arguments: --runtime-diff

@z-github2030 ➜ /workspaces/cli_diff (main) $ python3 v1 --runtime_diff commands_line.txt 
Expected runtime_difftime = 5 sec

Traceback (most recent call last):
  File "/workspaces/cli_diff/v1", line 73, in <module>
    main()
  File "/workspaces/cli_diff/v1", line 68, in main
    asyncio.runtime_diff(runtime_diff_commands_line(commands_line))
    ^^^^^^^^^^^^^^^^^^^^
AttributeError: module 'asyncio' has no attribute 'runtime_diff'
@z-github2030 ➜ /workspaces/cli_diff (main) $ ^C
@z-github2030 ➜ /workspaces/cli_diff (main) $ python3 v1 --runtime_diff commands_line.txt 

Expected runtime_difftime = 5 sec
[run_cli] interfaces (duration 2s)
[run_cli] inventory (duration 1s)
[complete_cli] inventory
[complete_cli] interfaces
[run_cli] bgp_summary (duration 3s)
[complete_cli] bgp_summary
Actual runtime_difftime = 5.01 sec (diff +0.01)
@z-github2030 ➜ /workspaces/cli_diff (main) $ 
