# QBCore Progressbar by QBHub

This is the QBCore Progressbar edited by QBHub and inspired by NoPixel 4.0.

![Screenshot 2024-01-06 175641](https://github.com/QBHub/progressbar/assets/47999933/93ffa56f-215e-4138-a667-ae3be2de6aab)
![Screenshot 2024-01-06 174953](https://github.com/QBHub/progressbar/assets/47999933/bb656b22-017a-411a-bb7a-6196fab0844a)

# Ox_lib integration tutorial

### To integrate QBCore progressbar into ox_lib:

- First, navigate to `ox_lib/resource/interface/client/progress.lua`.
- Locate the `function lib.progressBar(data)` within the file.
- Replace the entire code of this function with the following:

```lua
function lib.progressBar(data)
    while progress ~= nil do Wait(0) end

    if not interruptProgress(data) then
        playerState.invBusy = true
        exports['progressbar']:Progress({
            name = "random_task",
            duration = data.duration,
            label = data.label,
            useWhileDead = false,
            canCancel = true,
            controlDisables = {
                disableMovement = false,
                disableCarMovement = false,
                disableMouse = false,
                disableCombat = false,
            },
        }, function(cancelled)
            if not cancelled then
                -- The task has been completed
            else
                -- The task has been cancelled
                print("Cancelled")
            end
            progress = nil
            playerState.invBusy = false
        end)

        return startProgress(data)
    end
end


Progressbar
A dependency for creating progressbars in QB-Core frameworks.

Usage
QB-Core Functions
Client
QBCore.Functions.Progressbar(name, label, duration, useWhileDead, canCancel, disableControls, animation, prop, propTwo, onFinish, onCancel): Creates a new progressbar using QB-Core's built-in functions.

For example:
QBCore.Functions.Progressbar("random_task", "Doing something", 5000, false, true, {
    disableMovement = false,
    disableCarMovement = false,
    disableMouse = false,
    disableCombat = true,
}, {
    animDict = "mp_suicide",
    anim = "pill",
    flags = 49,
}, {}, {}, function()
    -- Task completed
end, function()
    -- Task cancelled
end)


Exports
Client
Progress(data, handler): Directly creates a new progressbar. It's recommended to use QB-Core's built-in function whenever possible.

For example:
exports['progressbar']:Progress({
    name = "random_task",
    duration = 5000,
    label = "Doing something",
    useWhileDead = false,
    canCancel = true,
    controlDisables = {
        disableMovement = false,
        disableCarMovement = false,
        disableMouse = false,
        disableCombat = true,
    },
    animation = {
        animDict = "mp_suicide",
        anim = "pill",
        flags = 49,
    },
    prop = {},
    propTwo = {}
}, function(cancelled)
    if not cancelled then
        -- Task completed
    else
        -- Task cancelled
    end
end)


isDoingSomething(): Checks if a progressbar is active.

For example:
local busy = exports["progressbar"]:isDoingSomething()

The rest of the functions follow the same structure as the examples provided above. For further details, refer to the specific documentation within the progressbar resource.


Please ensure to replace the screenshot URLs with the correct paths to the images in your repository.

