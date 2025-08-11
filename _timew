#compdef _timew timew

# zsh completion for timewarrior 1.7.1
# timewarrior_zsh_completion v0.1.0

_timew() {
    local ret=1

    _arguments -C \
        '1:command:->commands' \
        '*:ids_tags_hints:->ids_tags_hints' && ret=0

    case "$state" in
        commands)
            _describe 'commands' _commands
            ;;
        ids_tags_hints)
	    local arr vals

	    arr=()
	    # collected all tags from the database
	    vals=( "${(z)$(timew get dom.tracked.tags :all)}" )

            # add all of the tags to the output array
            for i in ${vals[@]}; do
		# strip out possible single double quotes from
		# multi-word tags
		arr+=( "$(echo $i | tr -d \" | tr -d \')" );
	    done

	    # collect interval ids and associated tags.

	    # iterate over the last 9 intervals
	    for n in {1..9}; do
		interval_tags=()

		# try and get the n-th interval tag count
		m_tags=$(timew get dom.tracked.${n}.tag.count 2>/dev/null)

		# if the interval wasn't found, exit loop
		if (( $? == 255 )); then
		    break
		fi

		# iterated over the m tags of interval n
		for m in {1..$m_tags}; do
		    tag=$(timew get dom.tracked.${n}.tag.${m} 2>/dev/null)
		    interval_tags+=("$tag")
		done
		arr+="@${n}:${interval_tags[@]}"
	    done

	    # append the predefined hints to the end
            arr+=( "${_hints[@]} ")

            _describe 'hints_tags_ids' arr
            ;;
    esac
}

_hints=(
    "\:adjust:Automatically correct overlaps"
    "\:blank:Leaves tracked time out of a report"
    "\:color:Force color on, even if not connected to a TTY"
    "\:day:The 24 hours of the current day"
    "\:debug:Runs in debug mode, shows many runtime details"
    "\:fill:Expand time to fill surrounding available gap"
    "\:ids:Displays interval ID numbers in the summary report"
    "\:lastmonth:Last month"
    "\:lastquarter:Last quarter"
    "\:lastweek:Last week"
    "\:lastyear:Last year"
    "\:month:This month"
    "\:nocolor:Force color off, even if connected to a TTY"
    "\:quarter:This quarter"
    "\:quiet:Turns off all feedback. For automation"
    "\:week:This week"
    "\:year:This year"
    "\:yes:Overrides confirmation by answering \'yes\' to the questions"
    "\:yesterday:The 24 hours of the previous day"
)

_commands=(
    'annotate:add an annotation to intervals'
    'cancel:cancel time tracking'
    'config:get and set Timewarrior configuration'
    'continue:resume tracking of existing interval'
    'day:Summarize the tracked and untracked time over the day'
    'day:shows a chart depicting a single day (today by default)'
    'delete:delete intervals'
    'diagnostics:show diagnostic information'
    'export:export tracked time in JSON'
    'extensions:list available extensions'
    'fill:adjust intervals to fill in surrounding gaps'
    'gaps:display time tracking gaps'
    'get:display DOM values'
    'help:display help'
    'join:join intervals'
    'lengthen:lengthen intervals'
    'modify:change start or end date of an interval'
    'month:Summarize the tracked and untracked time over a month'
    'month:shows a chart depicting a single month (current month by default)'
    'move:change interval start-time'
    'report:run an extension report'
    'resize:set interval duration'
    'retag:replace all tags in intervals'
    'shorten:shorten intervals'
    'show:display configuration'
    'split:split intervals'
    'start:start time tracking'
    'stop:stop time tracking'
    'summary:display a time-tracking summary'
    'tag:add tags to intervals'
    'tags:display a list of tags'
    'track:add intervals to the database'
    'undo:revert the last Timewarrior command'
    'untag:remove tags from intervals'
    'week:shows a chart depicting a single week (current week by default)'
)
