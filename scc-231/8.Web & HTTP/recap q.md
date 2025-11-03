### ![[Pasted image 20251103030902.png]]**1️⃣ What is the status code of the response?**

На скриншоте видно строку:

`< HTTP/2 304`

➡️ **Status code: 304 (Not Modified)**

---

### **2️⃣ Why does the server not return content in the HTTP response?**

Код состояния `304 Not Modified` означает, что:

> Содержимое ресурса **не изменилось** с момента, указанного в заголовке `If-Modified-Since`.

Поэтому сервер **не отправляет тело ответа (контент)**, а сообщает клиенту, что можно использовать кэшированную версию.

➡️ **Ответ:** сервер не возвращает контент, потому что ресурс не был изменён с последнего запроса, и клиент может использовать локальную копию.

---

### **3️⃣ Based on the provided headers, how long can a cache server store the object?**

В ответе видим строку:

`< cache-control: max-age=86400`

`max-age=86400` означает, что объект можно хранить в кэше **86400 секунд = 24 часа (1 день)**.

➡️ **Ответ:** кэш-сервер может хранить объект **24 часа**.

---

✅ **Итоговые ответы:**

1. Status code → `304 Not Modified`
    
2. No content → Ресурс не изменился с последнего запроса (`If-Modified-Since`)
    
3. Cache lifetime → `86400 секунд` (24 часа)


4. Describe how Web caching can reduce the delay in receiving a requested object. Will Web caching reduce the delay for all objects requested by a user or for only some of the objects? Why?

**Web caching reduces delay** by storing copies of frequently requested web objects closer to users, allowing subsequent requests to be served locally instead of contacting the remote server.  
However, it only reduces delay for **objects already cached and still valid** — new or infrequently requested objects must still be fetched from the origin server, providing no delay benefit.