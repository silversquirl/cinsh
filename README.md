# cinsh

CI system in POSIX sh

## Usage

`cinsh TASK_NAME`

Tasks are stored in `.cinsh/task/`, and are represented as directories containing
at least a `run` and `conf` file. The `run` file for a task should be an executable
file that can be run as a program within the specified container.  The `conf` file
is a configuration file, with each line taking the form `OPTION ARG1 ARG2 ...`

The following configuration options are supported:

- `container URL` - Specifies which container image to use for executing this task
- `dep TASK FILENAME` - Specifies that this task depends on a file or directory
  from another task's execution

When a task is executed, the contents of its directory is copied into `/cinsh/` on
the container. Any files specified by a `dep` option in the `conf` file will then
be copied in on top, possibly replacing existing files.
