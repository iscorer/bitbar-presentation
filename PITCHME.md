## The Problem

@css[fragment](Too much information)

@img[fragment](https://media.giphy.com/media/3o6gDSdED1B5wjC2Gc/giphy.gif)

---

## The Problem

@css[fragment](How can we more easily consume only the information we're interested in?)

@css[fragment](So we can take action on it.)

@css[fragment](And help prevent...)

@img[fragment](https://media.giphy.com/media/R0kVcQUow2Xtu/giphy.gif)

---

## More Specifically...

@css[fragment](Here's a problem I wanted to solve...)

@css[fragment](I wanted to know...)

@css[fragment](How many Tickets have I replied to?)

@css[fragment](- This week)

@css[fragment](- Today)

@css[fragment](- This hour)

@css[fragment](Am I hitting targets? *Am I doing OK?*)

---

## One Potential Solution

![BitBar](template/img/bitbar.png)

---

## What is BitBar?

BitBar lets you put the output of any script or program right in your Mac's Menu Bar

![BitBar Preview](template/img/bitbar-preview.png)

---

## How can BitBar help?

@css[fragment](The MacOS Menu Bar is a convenient and accessible place to display information.)

@css[fragment](BitBar lets *you* choose the information *you want to see* in the Menu Bar.)

@css[fragment](You can tell BitBar *when* to update the information it displays.)
@css[fragment](
```
10s - ten seconds
1m - one minute
2h - two hours
1d - a day
```
)

---

## How does it work?

- Write a simple script or run a program which outputs something
- Use pretty much any language you like
- It could be as simple as...
```bash
echo "Hello Zapier!"
```
- Or something a little more useful...
```bash
# Help Scout reply data variables
declare help_scout_replies_week=$(curl -s -u $help_scout_api_key:X "$help_scout_url?start=$start_date_this_week&end=$end_date_this_week&viewBy=day&user=$help_scout_user_id")
declare help_scout_replies_hour=$(curl -s -u $help_scout_api_key:X "$help_scout_url?start=$start_date_this_hour&end=$end_date_this_hour&viewBy=day&user=$help_scout_user_id")

# Help Scout reply count variables (extracted from JSON API response data using 'jq')
declare count_hs_replies_week=$(echo $help_scout_replies_week | /usr/local/bin/jq -j -s 'map(.current[].replies) | add')
declare count_hs_replies_day=$(echo $help_scout_replies_week | /usr/local/bin/jq -j ".current[] | select(.date==\"$date_today_zero_hours\").replies")
declare count_hs_replies_hour=$(echo $help_scout_replies_hour | /usr/local/bin/jq -j '.current[0].replies')

echo "Tickets: Hour $count_hs_replies_hour - Day: $count_hs_replies_day -  Week: count_hs_replies_week | size=12"
```
- Anything that can write to *standard out* is supported, so you can use Shell scripting, Python, JavaScript, Ruby, Shell, and more...

---

## Useful things you can do

- Get some data from a REST API
```bash
# 'curl' is a command-line tool for transferring data from or to a servers
curl https://api.helpscout.net/v1/reports/user/replies.json
```
- Transform that data (query it, do math on it)
```bash
# 'jq' is a command-line tool for transforming JSON data
cat data | jq -j ".current[] | select(.date==\"$date_today_zero_hours\").replies"
```
- Make pretty graphs from the data
```bash
# gnuplot is a command-line tool for generating graphs
cat data | gnuplot -p -c plot.gnu
```
- Display that information in the Menu Bar

---

## How I use BitBar

Simple script which shows me the time now in UTC
Find this really helpful when looking at logs

![UTC Timestamp](template/img/timestamp-napkin.png)

---

## What I've been working on (TicketBar)

![TicketNumbers](template/img/ticket-numbers.png)

![TicketBar](template/img/ticket-bar-r2.png)

![TicketBar](template/img/ticket-bar-r3.png)

![TicketBar](template/img/ticket-bar-actual.png)

## What I'm aiming for

![TicketBar](template/img/ticket-bar-mock.png)

---

## Over to you

- Install it
- Install some plugins
- Check out the BitBar docs
- Build something yourself
- Or help me with TicketBar!

---

## Resources

-- BitBar
-- BitBar (GitHub)
-- BitBar Plugins
-- TicketBar (GitHub)

---

## Questions?