# go-timewheel

golang timewheel lib, similar to golang std timer

## Usage

### base method

init timewheel

```go
tw, err := NewTimeWheel(1 * time.Second, 360)
if err != nil {
    panic(err)
}

tw.Start()
tw.Stop()
```

safe ticker

```go
tw, _ := NewTimeWheel(1 * time.Second, 360, TickSafeMode())
```

use sync.Pool

```go
tw, _ := NewTimeWheel(1 * time.Second, 360, SetSyncPool(true))
```

add delay task

```go
task := tw.Add(5 * time.Second, func(){})
```

remove delay task

```go
tw.Remove(task)
```

add cron delay task

```go
task := tw.AddCron(5 * time.Second, func(){
    ...
})
```

### similar to std time

similar to time.Sleep

```go
tw.Sleep(5 * time.Second)
```

similar to time.After()

```go
<- tw.After(5 * time.Second)
```

similar to time.NewTimer

```go
timer :=tw.NewTimer(5 * time.Second)
<- timer.C
timer.Reset(1 * time.Second)
timer.Stop()
```

similar to time.NewTicker

```go
timer :=tw.NewTicker(5 * time.Second)
<- timer.C
timer.Stop()
```

similar to time.AfterFunc

```go
runner :=tw.AfterFunc(5 * time.Second, func(){})
<- runner.C
runner.Stop()
```

## benchmark test

[example/main.go](example/main.go)
