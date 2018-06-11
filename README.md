Luakit
-----------------------------

A multi-platform solution in lua , you can develop your app, IOS or android app with this tool, truely  write once , use everywhere. Notice , you can only use Luakit to write business logic code including network, db orm,  multithread model, but not UI code, Luakit do not provide api for UI development.

Why write apps with Luakit?
-----------------------------

I will say Luakit is the most effective tool to develop apps on more than one platform. Here are some reasons

* Cross platform, truely write once use everywhere, this feature is very attractive, if you have experienced multi-platform development , cross platform architecture will be very impressive for you. It can promote efficiency largely.

* Dynamic and flexible, write business logic code in lua , you can release your code anytime, truely agile development.

* Forget the annoying memory management, lua support automatic garbage collection. Lua has closures, also known as blocks. These features make Luakit much more effective than other c++ cross platform solution.

Examples
-----------------------------

For some simple Luakit apps, check out the [source folder](https://github.com/williamwen1986/Luakit/tree/master/LuaKitProject).

**Multithreading**

We provide some powerful multi-threading api in lua , you can see ThreadTest in Android Demo folder and IOS Demo folder. Notice , It is not only thread safety multithreading model, but also really competition multithreading model. It is the unique solution to perform competition multithreading in lua or js.

Create thread , [demo code](https://github.com/williamwen1986/Luakit/blob/master/LuaKitProject/src/Projects/LuaSrc/thread_test.lua)
```lua
-- Parma1 is the thread type ,there are five types of thread you can create.
-- BusinessThreadUI
-- BusinessThreadDB
-- BusinessThreadLOGIC
-- BusinessThreadFILE
-- BusinessThreadIO
-- Param2 is the thread name
-- Result is new threadId which is the token you should hold to do further action
local newThreadId = lua.thread.createThread(BusinessThreadLOGIC,"newThread")
```

Perform method on a specified thread async, [demo code](https://github.com/williamwen1986/Luakit/blob/master/LuaKitProject/src/Projects/LuaSrc/thread_test.lua)
```lua
-- Parma1 is the threadId for which you want to perform method
-- Parma2 is the modelName
-- Parma3 is the methodName
-- The result is just like you run the below code on a specified thread async
-- require(modelName).methodName("params", 1.1, {1,2,3}, function (p)
-- end)
lua.thread.postToThread(threadId,modelName,methodName,"params", 1.1, {1,2,3}, function (p)
	-- do something here
end)
```

Perform method on a specified thread sync, [demo code](https://github.com/williamwen1986/Luakit/blob/master/LuaKitProject/src/Projects/LuaSrc/thread_test.lua)
```lua
-- Parma1 is the threadId for which you want to perform method
-- Parma2 is the modelName
-- Parma3 is the methodName
-- The result is just like you run the below code on a specified thread sync
-- local result = require(modelName).methodName("params", 1.1, {1,2,3}, function (p)
-- end)
local result = lua.thread.postToThreadSync(threadId,modelName,methodName,"params", 1.1, {1,2,3}, function (p)
	-- do something here
end)
```

**ORM**

Luakit provide a orm solution which has below features

* Object-oriented interfaces
* Automatically create and update table schemas.
* Has internal cache
* Timing auto transaction
* Thread safe

Define your model, [demo code](https://github.com/williamwen1986/Luakit/blob/master/LuaKitProject/src/Projects/LuaSrc/db_test.lua)
```lua
-- Add the define table to dbData.lua
-- Luakit provide 7 colum types
-- IntegerField to sqlite integer 
-- RealField to sqlite real 
-- BlobField to sqlite blob 
-- CharField to sqlite varchar 
-- TextField to sqlite text 
-- BooleandField to sqlite bool
-- DateTimeField to sqlite integer
user = {
		__dbname__ = "test.db",
	    __tablename__ = "user",
	    username = {"CharField",{max_length = 100, unique = true, primary_key = true}},
	    password = {"CharField",{max_length = 50, unique = true}},
	    age = {"IntegerField",{null = true}},
	    job = {"CharField",{max_length = 50, null = true}},
	    des = {"TextField",{null = true}},
	    time_create = {"DateTimeField",{null = true}}
	},
-- when you use, you can do just like below
local Table = require('orm.class.table')
local userTable = Table("user")
```

Insert data, [demo code](https://github.com/williamwen1986/Luakit/blob/master/LuaKitProject/src/Projects/LuaSrc/db_test.lua)
```lua
local userTable = Table("user")
local user = userTable({
		username = "user1",
        password = "abc",
        time_create = os.time()
})
user:save()
```

Comming soon......
-----------------------------
