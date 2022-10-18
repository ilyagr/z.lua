With BUG.zlua in db,
```
cd ~/stow/local/.local/bin
z -e -b local dotfiles
```
results in `/bin` instead of anything reasonable.

The above is equivalent to `z -e ~/stow/local/. dotfiles /bin`.
The problem is around the line 1600 of `z.lua`, in the following code:

```lua
	if os.path.isabs(last) and os.path.isdir(last) then
		local size = #patterns
		if size <= 1 then
			return os.path.norm(last)
		elseif last ~= '/' and last ~= '\\' then
			return os.path.norm(last)
		end
	end
```

In this case, `last` is `/bin` and early return happens.