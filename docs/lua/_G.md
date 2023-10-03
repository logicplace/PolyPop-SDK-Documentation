# The global scope

The global scope is represented by the global variable `_G` of type `table` containing the following members.

- __tself - Type: userdata
- __weaktable - Type: table
- [_G](#the-global-scope)
- _VERSION - Type: string
- Antimatter - Type: table
- box_ - Type: table
- browser_port - Type: number
- Core - Type: table
- coroutine - Type: table (a library)
- d - Type: number
- Exception - Type: table
- io - Type: table (a library)
- json - Type: table
- lvi - Type: table
- math - Type: table (a library)
- matrix_ - Type: table
- nearest_block - Type: number
- os - Type: table (a library)
- package - Type: table (a library)
- plane_ - Type: table
- poll_timer_id - Type: number
- PollTimer - Type: table
- PolyPop - Type: table
- Promise - Type: table
- quaternion_ - Type: table
- ray_ - Type: table
- Repromise - Type: table
- RequestPool - Type: table
- RequestQueue - Type: table
- segment_ - Type: table
- string - Type: table (a library)
- sphere_ - Type: table
- table - Type: table (a library)
- Time_ - Type: table
- val - Type: number
- vector2_ - Type: table
- vector3_ - Type: table
- vector4_ - Type: table

- ampTodB(???)
- approx_eq(???)
- approxEquals(???)
- assert(cond [,"error msg"]) -- verifies the condition is true or breaks at the line with the given error message
- base64encode(???)
- box(min, max) -- axis-aligned box represented by a min and max point
- collectgarbage(???)
- createPromise(???)
- createRepromise(???)
- dBToAmp(???)
- distance(???)
- dofile(???)
- encodeURI(???)
- error("msg") -- stops play and breaks at the line with the given error message
- exists(obj) -- returns true if the given object is valid or false if it's nil or the object has been deleted
- fetch(???)
- fromhsb({h=180,s=0.5,b=1}) -- returns a vector4 color from hue/saturation/brightness values H[0,360] S[0,1] B[0,inf]
- generateGUID(???)
- getAxisRotationMatrix(???)
- getAnimator(???)
- getAppVersion(???)
- [getEditor()](#geteditor)
- getGraphics(???)
- getHub(???)
- getInput(???)
- getLocalFolder(???)
- getmetatable(???)
- getNetwork(???)
- getNormalRotationMatrix(???)
- getOS(???)
- getRotationMatrix(???)
- getRotationXMatrix(???)
- getRotationYMatrix(???)
- getRotationZMatrix(???)
- getScalingMatrix(???)
- getTranslationMatrix(???)
- getUI(???)
- [getUniverse()](#getuniverse)
- hash(???)
- hash_hmac(???)
- hours(h)
- ipairs(???)
- jsonify(???)
- jsonify_test(???)
- kit(???)
- kit_iter(???)
- lerp(???)
- load(???)
- loadfile(???)
- log(???)
- matrix() -- 4x4 row/column matrix (defaults to an identity matrix)
- minutes(m)
- milliseconds(ms)
- next(???)
- noise(v) -- where v is a 1/2/3d value, returns a smoothed random value [-1,1] across the given dimensions
- openWebLink(???)
- pairs(???)
- pcall(???)
- plane(a,b,c,d) -- a plane defined by the equation ax+by+cz+d=0
- polltimer(???)
- print("msg") -- prints a message to the console
- quaternion(x,y,z,w) -- a quaternion to represent rotations about an axis
- queryStringToTable(???)
- queue(???)
- rawequal(???)
- rawget(???)
- rawlen(???)
- rawset(???)
- ray(point, direction) -- a ray define by a point and a normalized direction
- refetch(???)
- requestpool(???)
- requestqueue(???)
- require(???)
- require_org(???)
- rgba("ff0084ff") -- returns a vector4 color from an rgba hex color
- rgba(255,0,132,255) -- returns a vector4 color from 32bit rgba color values
- round(???)
- seconds(s)
- segment(point1, point2) -- a segment defined by two points
- select(???)
- setmetatable(???)
- spectralnoise(???)
- sphere(point, radius) -- sphere represented by a point and a radius
- split(???)
- throw(???)
- time(???)
- tohex(???)
- tohsb(v4) -- returns a table of {h,s,b} (loses alpha)
- tonumber(n) -- converts a string to numeric value 
- tostring(obj) -- converts a type to a string representation (e.g. "true", "23.0", "x:3 y:4 z:2", etc)
- type(obj) -- This function will return a string identifying a Lua type (i.e. "number"), additional built-in type (i.e. "vector3"), or Simmetri object type (i.e. "MeshEntity")
- vector2(x,y) -- 2 component vector
- vector3(x,y,z) -- 3 component vector
- vector4(x,y,z,w) -- 4 component vector
- warn(???)
- xpcall(???)

## Other global functions not in _G

- Instance - Type: table

- event(???)
- findObjectByUid("^1/14WA1O27OBRZY3805NLB9767IZ")
- properties(???)
- resolvePath(???)

## getEditor ()

Return the top-level (or current?) [PolyPopEditor](PolyPopEditor.md) object.

## getUniverse ()

Return the [Universe](Universe.md) object.

TODO: what's it for? no idea


## time

```lua
t = milliseconds(ms), seconds(s), minutes(m), hours(h) -- time
```
