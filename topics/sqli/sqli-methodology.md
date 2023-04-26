# SQL Injection Methodology/Workflow

## Your entire attack depends on whether the ending termination of query character(s) are accepted by the RDMS.

Is this true? PS Labs rejected my otherwise valid UNION attacks because I ended my query with `--` instead of `#`. I think that's kind of BS and not realistic.
