---
ID: 511
post_title: >
  BASH. How To Create Multi-line CASE
  Statement
author: sunsingerus
post_excerpt: ""
layout: post
permalink: >
  https://sunsingerus.com/bash-how-to-create-multi-line-case-statement/
published: true
post_date: 2018-07-17 11:11:05
---
What if you'd like to have multi-line case statement?
Here is an example:
<pre>
#!/bin/bash

A=C

case "$A" in
        A | \
        B | \
        C )
                echo $A
                ;;
        *)
                echo "Unknown"
                ;;
esac
</pre>
Mainly, it is multi-line version of
<pre>
case "$A" in
        A | B | C )
                echo $A
                ;;
        *)
                echo "Unknown"
                ;;
esac
</pre>
and provides the most benefits when there are really many options to choose from, for example, like in this code sample

<pre>
case "$ITEM" in
        DiskUsage)
                du -sb "$CH_PATH" | awk '{print $1}'
                ;;

        Revision)
                cat  "$CH_PATH/status" | grep Revision | awk '{print $2}'
                ;;

        LongestRunningQuery)
                run_ch_process_command | sort | tail -1
                ;;

        DelayedInserts          | \
        HTTPConnection          | \
        InsertedBytes           | \
        InsertedBytes           | \
        InsertedRows            | \
        InsertQuery             | \
        MaxPartCountForPartition| \
        MemoryTracking          | \
        MergedRows              | \
        MergedUncompressedBytes | \
        Query                   | \
        Read                    | \
        ReadCompressedBytes     | \
        ReplicasMaxAbsoluteDelay| \
        ReplicasSumQueueSize    | \
        SelectedParts           | \
        SelectQuery             | \
        TCPConnection           | \
        Uptime                  | \
        Write                   | \
        ZooKeeperWatch          )
                run_ch_metric_command "$ITEM"
                ;;

        *)
                echo "Unknown argument '$ITEM'. Please check command to run"
                exit 1
                ;;
esac


</pre>