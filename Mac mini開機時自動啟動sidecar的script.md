---
created: 2022-02-03T08:51:14.264Z
modified: 2022-02-03T08:51:51.764Z
---
# Mac mini開機時自動啟動sidecar的script

好幾位版友寫信來跟我要這個script
這個script的用途是沒有外接螢幕時
把iPad當成mini的外接螢幕
但這樣做要克服一個問題
因為沒有外接螢幕
所以必須要在開機時自動啟動sidecar
讓mini能夠連接iPad當成螢幕使用

要注意我的ipad名稱就叫iPad
如果版友有別的命名要記得改

```
set deviceName to "iPad" -- Change this to the name of your iPad

set displayM
enu to "" -- Do not change this

tell application "System Events"
        tell its ap
plication process "ControlCenter"
                -- Get all menu bar items.
                set menuBarIt
ems to menu bar items of menu bar 1

                -- Determine if the Display menu is i
n the menu bar.
                repeat with mbi in menuBarItems
                        if name of mbi contains "
顯示器" then
                                set displayMenu to mbi
                        end if
                end repeat

                -- If the
Display menu is in the menu bar, get the Sidecar device.
                -- In Big Sur, it's
 a toggle button (checkbox) instead of a menu item.
                if displayMenu is not eq
ual to "" then
                        click displayMenu
                        set deviceToggle to checkbox 1 of scrol
l area 1 of group 1 of window "控制中心" whose title contains deviceName


                -- Click the device.
                        click deviceToggle

                        -- The menu name changes w
hen Sidecar is active, so we need to get the Display menu again, then click to
 close it.
                        set displayMenu to (first menu bar item whose name con
tains "顯示器") of menu bar 1
                        click displayMenu
                else
                        -- If the Display menu isn
't in the menu bar, display an error message.
                        set errorMessage to "Display
menu not found in menu bar. Open System Preferences > Dock & Menu Bar. Set Dis
play to \"Show in Menu Bar > Always.\""
                        display dialog errorMessage with ic
on caution
                end if
        end tell
end tell

```
--