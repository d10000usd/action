#!/bin/zsh

# Define ANSI escape codes
GREEN=$'\e[32m'
RESET=$'\e[0m'

# Kill processes on specified ports
kill -9 $(lsof -t -i :7001) 2>/dev/null
kill -9 $(lsof -t -i :1338) 2>/dev/null
kill -9 $(lsof -t -i :8088) 2>/dev/null

# Display messages with color
echo "${GREEN}server start for kill port 7001,1338,8088${RESET}"
echo "${GREEN}start server 7001,1338,8088 ${RESET}"

# Start backend server
cd /Users/hg/PROJECT/backend && uvicorn main:app_router.app --host 0.0.0.0 --port 7001 --reload &
# Start Vue.js development server
cd /Users/hg/PROJECT/frontend/hg-project-bootstrap && yarn serve &
# Start another server (example: reverse http-proxy-middleware Proxy)
cd /Users/hg/PROJECT/serverproxy && yarn start &

# Open web pages
echo "${GREEN}-------------------------------------------- web pages ${RESET}"
echo "${GREEN}-------------------------------------------- http-proxy-middleware start 7001 ${RESET}"
echo "${GREEN}-------------------------------------------- uvicorn start 7001 ${RESET}"
echo "${GREEN}-------------------------------------------- Vue.js start 8088 ${RESET}"
pages="http://172.30.1.10:8088/WebSearchView"
open "$pages"
echo "$pages"