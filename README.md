# WEEK 01: Submissions

## Evidence from the end of the module Create a web API with ASP.NET Core controllers:

### POST
REQUEST:
POST {{ContosoPizza_HostAddress}}/pizza/
Content-Type: application/json

{
    "name": "Criolla",
    "isGlutenFree": false
}

RESPONSE:
HTTP/1.1 201 Created
Connection: close
Content-Type: application/json; charset=utf-8
Date: Wed, 04 Nov 2026 19:41:00 GMT
Server: Kestrel
Location: http://localhost:5218/Pizza/3
Transfer-Encoding: chunked

{
  "id": 3,
  "name": "Criolla",
  "isGlutenFree": false
}

### PUT
REQUEST:
PUT {{ContosoPizza_HostAddress}}/pizza/3
Content-Type: application/json

{
    "id": 3,
    "name": "Criolla Uruguaya",
    "isGlutenFree": false
}

RESPONSE:
HTTP/1.1 204 No Content
Connection: close
Date: Wed, 04 Nov 2026 19:48:22 GMT
Server: Kestrel

### GET (showing additional pizza)
REQUEST:
GET {{ContosoPizza_HostAddress}}/pizza/
Accept: application/json

RESPONSE:
HTTP/1.1 200 OK
Connection: close
Content-Type: application/json; charset=utf-8
Date: Wed, 04 Nov 2026 19:50:36 GMT
Server: Kestrel
Transfer-Encoding: chunked

[
  {
    "id": 1,
    "name": "Classic Italian",
    "isGlutenFree": false
  },
  {
    "id": 2,
    "name": "Veggie",
    "isGlutenFree": true
  },
  {
    "id": 3,
    "name": "Criolla Uruguaya",
    "isGlutenFree": false
  }
]

### DELETE
REQUEST:
DELETE {{ContosoPizza_HostAddress}}/pizza/3

RESPONSE:
HTTP/1.1 204 No Content
Connection: close
Date: Wed, 04 Nov 2026 19:51:57 GMT
Server: Kestrel





### 3. Working Sales Summary Function

Below is the text copy of the working sales summary function from the "Work with files and directories in a .NET app" module.

```csharp
void CreateSummary()
{    
    File.WriteAllText(Path.Combine(salesTotalDir, "salesSummary.txt"), $"Sales Summary\n--------------------------------\n Details:\n");

    double total = 0;
    double totalByStore = 0;
    IEnumerable<string> allStoresTotals = Directory.EnumerateFiles("stores", "salestotals.json", SearchOption.AllDirectories);
    foreach (var file in allStoresTotals)
    {
        string salesJson = File.ReadAllText(file);
        TotalData? data = JsonConvert.DeserializeObject<TotalData?>(salesJson);

        // Add the amount found in the Total field to the salesTotal variable
        totalByStore = data?.OverallTotal ?? 0;
        total += totalByStore;
        File.AppendAllText(Path.Combine(salesTotalDir, "salesSummary.txt"), $"  {file}: ${totalByStore}{Environment.NewLine}");

    }
    File.AppendAllText(Path.Combine(salesTotalDir, "salesSummary.txt"), $"\n Total Sales: ${total}{Environment.NewLine}");
}
record TotalData(double OverallTotal);
```

### RESULT in the file: salesSummary.txt

```text
Sales Summary
--------------------------------
 Details:
 stores\201\salestotals.json: $1501,22
 stores\202\salestotals.json: $101,22
 stores\203\salestotals.json: $154401,22
 stores\204\salestotals.json: $13501,22

 Total Sales: $169504,88
```



