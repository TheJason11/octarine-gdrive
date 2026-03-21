```plaintext
@echo off
setlocal

REM ── 1) start LM Studio only if it isn’t already running ────────────────────────
tasklist /fi "imagename eq LM Studio.exe" | find /i "LM Studio.exe" > nul
if %errorlevel%==1 (
    echo ► Launching LM Studio …
    REM /min = new window, minimised; /d detaches it from this console
    start "" /min "C:\Users\Jason\AppData\Local\Programs\LM Studio\LM Studio.exe"
    timeout /t 12 > nul
) else (
    echo ► LM Studio is already running.
)

REM ── 2) move to your .agent folder ─────────────────────────────────────────────
cd /d "C:\Users\Jason\BeeLink_Notes\.agent"

REM ── 3) activate the venv ──────────────────────────────────────────────────────
call ".\.venv\Scripts\activate.bat"

REM ── 4) run the daily roll-up ──────────────────────────────────────────────────
echo ► Running daily_rollup.py …
call ".\.venv\Scripts\python.exe" daily_rollup.py 24

REM ── 5) show exit status & keep the window open ───────────────────────────────
echo ► Script finished with exit code %errorlevel%
pause
endlocal
```