# Figma MCP Setup & Troubleshooting

**Date**: December 3, 2024  
**Status**: WebSocket server running ✅

---

## Problem: "No server info found" Error

**Error Message**:
```
Handling ListOfferings action, server stored: false
No server info found
```

**Cause**: The TalkToFigma MCP server needs the WebSocket server (`cursor-talk-to-figma-socket`) to be running first.

---

## Solution: Two-Server Setup

TalkToFigma requires **two servers** to work:

### 1. WebSocket Server (Required First)
**Command**: `bunx cursor-talk-to-figma-socket`  
**Port**: 3055  
**Purpose**: Connects to Figma Desktop app via WebSocket

**Status**: ✅ Currently running

### 2. MCP Server (Connects to WebSocket Server)
**Command**: `bunx cursor-talk-to-figma-mcp`  
**Purpose**: Provides MCP interface to Cursor, connects to WebSocket server

**Status**: Configured in `~/.cursor/mcp.json`

---

## Setup Instructions

### Step 1: Install Bun (if not installed)
```bash
curl -fsSL https://bun.sh/install | bash
export PATH="$HOME/.bun/bin:$PATH"
```

### Step 2: Start WebSocket Server
```bash
# In a terminal (keep running):
bunx cursor-talk-to-figma-socket

# Or run in background:
bunx cursor-talk-to-figma-socket &
```

**Expected Output**:
```
WebSocket server running on port 3055
New client connected
```

### Step 3: Verify MCP Configuration

**File**: `~/.cursor/mcp.json`

**Current Configuration**:
```json
{
  "mcpServers": {
    "Figma Desktop": {
      "url": "http://127.0.0.1:3845/mcp"
    },
    "TalkToFigma": {
      "command": "bunx",
      "args": [
        "cursor-talk-to-figma-mcp@latest"
      ]
    }
  }
}
```

**This looks correct!** ✅

### Step 4: Restart Cursor

After starting the WebSocket server:
1. **Restart Cursor** to reload MCP servers
2. The TalkToFigma MCP should now connect to the WebSocket server
3. Check MCP status in Cursor settings

---

## Verification

### Check WebSocket Server
```bash
# Check if port 3055 is listening:
lsof -i :3055

# Should show:
# COMMAND   PID   USER   FD   TYPE   DEVICE SIZE/OFF NODE NAME
# bun     96749 larsen    5u  IPv6   ...    TCP *:policyserver (LISTEN)
```

### Check MCP Server
- Open Cursor Settings → MCP
- Look for "TalkToFigma" server status
- Should show "Connected" or "Running"

---

## Troubleshooting

### Error: "No server info found"

**Possible Causes**:
1. ❌ WebSocket server not running
2. ❌ WebSocket server on wrong port
3. ❌ MCP server started before WebSocket server
4. ❌ Cursor not restarted after starting WebSocket server

**Solutions**:
1. ✅ Start WebSocket server first: `bunx cursor-talk-to-figma-socket`
2. ✅ Wait for "WebSocket server running on port 3055"
3. ✅ Restart Cursor
4. ✅ Check MCP server logs in Cursor

---

### Error: "bunx: command not found"

**Solution**:
```bash
# Install Bun:
curl -fsSL https://bun.sh/install | bash

# Add to PATH:
export PATH="$HOME/.bun/bin:$PATH"

# Or use full path:
~/.bun/bin/bunx cursor-talk-to-figma-socket
```

---

### Error: "Port 3055 already in use"

**Solution**:
```bash
# Find process using port 3055:
lsof -i :3055

# Kill it:
kill -9 <PID>

# Or use different port (if supported):
# Check cursor-talk-to-figma-socket documentation
```

---

### MCP Server Not Connecting

**Check**:
1. WebSocket server is running (`lsof -i :3055`)
2. Cursor has been restarted
3. MCP configuration is correct (`~/.cursor/mcp.json`)
4. No firewall blocking localhost connections

**Restart Sequence**:
1. Stop WebSocket server (Ctrl+C)
2. Stop Cursor
3. Start WebSocket server: `bunx cursor-talk-to-figma-socket`
4. Wait for "WebSocket server running"
5. Start Cursor
6. Check MCP status

---

## Current Status

**WebSocket Server**: ✅ Running on port 3055  
**MCP Configuration**: ✅ Correct  
**Next Step**: Restart Cursor to connect MCP server

---

## Alternative: Use Figma Desktop MCP

If TalkToFigma continues to have issues, you can use the **Figma Desktop MCP** instead:

**Configuration** (already in `mcp.json`):
```json
"Figma Desktop": {
  "url": "http://127.0.0.1:3845/mcp"
}
```

**Requirements**:
- Figma Desktop app must be running
- Figma Desktop MCP plugin must be installed
- Server runs on port 3845

**We've been using this successfully** for our Figma analysis! ✅

---

## Which MCP to Use?

### Figma Desktop MCP ✅ (Currently Working)
- **Pros**: Direct connection, no WebSocket server needed
- **Cons**: Requires Figma Desktop app running
- **Status**: ✅ Working for our analysis

### TalkToFigma MCP ⚠️ (Needs Setup)
- **Pros**: More features, WebSocket-based
- **Cons**: Requires WebSocket server running first
- **Status**: ⚠️ Needs WebSocket server + Cursor restart

**Recommendation**: Continue using **Figma Desktop MCP** for now (it's working!), or set up TalkToFigma if you need its specific features.

---

## Quick Reference

### Start WebSocket Server
```bash
export PATH="$HOME/.bun/bin:$PATH"
bunx cursor-talk-to-figma-socket
```

### Check Server Status
```bash
lsof -i :3055  # WebSocket server
lsof -i :3845  # Figma Desktop MCP
```

### MCP Configuration Location
```
~/.cursor/mcp.json
```

---

**Last Updated**: December 3, 2024  
**WebSocket Server**: Running ✅  
**Action Required**: Restart Cursor to connect TalkToFigma MCP




