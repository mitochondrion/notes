```
====================
H4X021N9
====================
Route WiFi device through Charles Proxy
  Connect both machines to same network
  Set proxy on iPad to same IP as machine where Charles is running on port 8888

====================
GIT
====================
http://railsware.com/blog/2014/08/11/git-housekeeping-tutorial-clean-up-outdated-branches-in-local-and-remote-repositories/

Clean local branches
  git branch
  git co develop
  git branch --merged
  git branch -d [MERGED BRANCH TO DELETE]
  git branch --no-merged
  git branch -D [UN-MERGED BRANCH TO DELETE]

Clean remote branches
  git fetch -p (OR git remote prune origin)
  git branch -r
  git branch -r --merged
  git push origin --delete [REMOTE BRANCH TO DELETE]

List remote merged branches
  Merged
    for branch in `git branch -r --merged | grep -v HEAD`; do echo -e `git show --format="%ci %cr %an" $branch | head -n 1` \\t$branch; done | sort -r
  Un-merged
    for branch in `git branch -r --no-merged | grep -v HEAD`; do echo -e `git show --format="%ci %cr %an" $branch | head -n 1` \\t$branch; done | sort -r

Remove a pushed /Pods folder
  git filter-branch --index-filter 'git rm --cached --ignore-unmatch Pods/*' --tag-name-filter cat -- --all
  git push --force

====================
UNIX
====================
netcat
  nc -l 8080

OSX kernel resources
  Processes
    sysctl -a | grep maxproc
    sudo sysctl -w kern.maxproc=2500
    sudo sysctl -w kern.maxprocperuid=2048

  Files Handles
    sysctl -a | grep files
    sudo sysctl -w kern.maxfiles=12288
    sudo sysctl -w kern.maxfilesperproc=10240

  Sockets
    sysctl -a | grep somax
    sudo sysctl -w kern.ipc.somaxconn=2048

  ulimit -n 10240

Current File Handle Counts
  lsof | awk '{print $1}' | uniq -c | sort -rn | head

Hammer Time
  while true; do ps aux | grep curl | wc -l; sleep .2; done
  while true; do curl -NSso /dev/null -w "%{http_code}\n" [ENDPOINT] >> /tmp/node_hammer_status & done
  time for i in {1..10000}; do curl -NSso /dev/null [ENDPOINT] & done
  psef curl | wc -l

Zombies
  ps aux | awk '"[Zz]" ~ $8 { printf("%s, PID = %d\n", $8, $2); }'

Overwrite previous line
  Append carriage return "\r" without a new line
  OR wipe out entire line with "\x1b[2K\r"

====================
ANDROID
====================
~/Library/Android/sdk/platform-tools/adb
adb install [path to .apk]

~/Library/Android/sdk/tools/emulator -avd Nexus_6_API_23 -netspeed full -netdelay none -http-proxy http://127.0.0.1:8888 -port 5554

###Clean gradle cache
* `rm -rf ~/.gradle/caches`
* `rm -rf [ProjectRoot]/.gradle`
* `[ProjectRoot]/gradlew assemble`

===================
GROOVY
===================
Object to JSON
  import groovy.json.*
  new JsonBuilder(object).toPrettyString()


Slurp ChildNode to XML
  import groovy.xml.XmlUtil
  groovy.xml.XmlUtil.serialize(node).toString()


==================
OSX
==================
Remote Login (SSH) Address
  dns-sd -B _ssh._tcp

```
