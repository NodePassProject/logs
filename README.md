# Logs Package

[![Go Reference](https://pkg.go.dev/badge/github.com/NodePassProject/logs.svg)](https://pkg.go.dev/github.com/NodePassProject/logs)
[![License](https://img.shields.io/badge/License-BSD_3--Clause-blue.svg)](https://opensource.org/licenses/BSD-3-Clause)

A simple, flexible, and thread-safe logging system for Go applications.

## Features

- Thread-safe logging with mutex protection
- Multiple log levels (Debug, Info, Warn, Error, Event)
- Customizable minimum log level
- Colored terminal output (optional)
- Custom timestamp formatting
- Standard library compatibility through `log.Logger` adapter

## Installation

```bash
go get github.com/NodePassProject/logs
```

## Usage

### Basic Usage

```go
package main

import (
    "github.com/NodePassProject/logs"
)

func main() {
    // Create a new logger with INFO minimum level and color enabled
    logger := logs.NewLogger(logs.Info, true)
    
    // Log messages at different levels
    logger.Debug("This debug message won't be shown because minimum level is INFO")
    logger.Info("System started successfully")
    logger.Warn("Configuration file not found, using defaults")
    logger.Error("Failed to connect to database: %s", "connection timeout")
    logger.Event("System event: application state changed")
}
```

### Changing Log Level at Runtime

```go
// Create logger with INFO level
logger := logs.NewLogger(logs.Info, true)

// Later change to DEBUG level
logger.SetLogLevel(logs.Debug)

// Get current log level
currentLevel := logger.GetLogLevel()
```

### Disabling Colors

```go
logger := logs.NewLogger(logs.Info, true)

// Disable colored output
logger.EnableColor(false)
```

### Using with Standard Library

```go
logger := logs.NewLogger(logs.Info, true)

// Get a standard library logger that uses our custom logger
stdLogger := logger.StdLogger()

// Use standard logger methods
stdLogger.Println("This message will be logged through our custom logger")
stdLogger.Printf("Formatted %s", "message")
```

## License

Copyright (c) 2025, NodePassProject. Licensed under the BSD 3-Clause License.
See the [LICENCE](LICENCE) file for details.