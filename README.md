This project is in developing...

Yet another CouchDB GO Client

0.1 is for core API

## Quick start

    // Client is your friend
    // Use Client everywhere you want :)

    import (
        "github.com/GuoJing/gocouchDB"
    )

    dsn := "http://localhost:5984"
    client := gocouchDB.NewClientByDSN(dsn)

    db, err := client.GetDatabase("duidui")

    if err != nil {}

    doc, err := db.GetDocument("test")

    body := map[string]interface{} {
        "title" : "Haha223334444",
        "body"  : "Not at all",
    }

    doc.Update(body)

    // Or
    // doc.Delete()

## Transport

    //interface ITransport! <- you can do it yourself
    transport := NewTransport(dsn)

    client := gocouchDB.NewClientByTransport(transport)

## Visit without Client

    transport := NewTransport(dsn)
    db := NewDatabase(dbName, transport)
    doc, err := db.GetDocument(Name)

    doc = NewDocument(dbName, Name, transport)
    doc.Delete()

## Auth

    client := gocouchDB.NewClientByDSN(dsn)
    client.SetAuth(Username, Password)
    client.GetDatabase("duidui")
    // ...

    // or

    transport := NewTransport(dsn)
    db := NewDatabase(dbName, transport)
    db.SetAuth(Username, Password)
    db.GetDocument("doc")
    // ...

## Replicate

    task := new(gocouchDB.ReplicateTask)
    task.Continuous = false
    task.CreateTarget = true
    task.Source = "duidui"
    task.Target = "duidui_backup"

    ret, err := client.Replicate(task)


## do function

    // You could do anything with do
    // this is ClientBase
    // you can do that in every Class
    // like Database, Document...
    // Here we call this cl
    // if we need a couchdb interface like:
    // dsn/_replicate?param1=value1

    body = map[string]interface{} {
        "source": "source_db",
        "target": "target_db",
    }

    params = map[string]string {
        "param1": "value1"
    }

    cl.do(POST, "_replicate", body, params)

    // you could see Compact in Database class
    // everything is using do function (but _all_dbs)
