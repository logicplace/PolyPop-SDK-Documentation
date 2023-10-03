# Enum

Subclass of BasicProperty ??

## clearElements ()

## getElementCount ()

Return an integer representing the number of elements in the Enum.

## getElements (out)

Retrieve the allowed elements and put them into out.

```lua
local t = {}
enum:getElements(t)
for k,v in pairs(t) do	
	print(k .. ": " .. v)
end
--[[
	If enum's elements are "Cat" and "Dog" this will print:
	1: Cat
	2: Dog
]]
```

## getValue ()

Return current value of the property.

## getValueIndex ()

Return an integer representing the index of the current value corresponding to its order in the Enum's elements.

For example if the Enum has the elements `"Cat"` and `"Dog"` and the current value is `"Dog"`, this function will return `2`.

## hasElement (element)

Returns true if element is allowed in this Enum, false otherwise.

## isValueMissing ()

## setElements (elements, keep_value, current)

- elements: A sequential table containing the elements this Enum allows
- keep_value: Boolean denoting if it should attempt to (?) keep the pre-existing value
  - optional, default: ?
- current: Set the new current value after updating the elements
  - optional, behavior is ???

## setValue (v)

Set the current value to v.

TODO: What happens if it's not a member of the Enum?

## setValueByIndex (i)

Set the current value by the index corresponding to the order in the Enum's elements.

For example if the Enum has the elements `"Cat"` and `"Dog"`, `setValueByIndex(2)` will set the current value to `"Dog"`.
