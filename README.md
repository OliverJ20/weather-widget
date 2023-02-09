# weather-application

![Screenshot](/Screenshot%20from%202023-02-09%2015-05-12.png)
## Task
The task was to create a small widget which will use data from a public API to display current weather for either Brisbane, Sydney or Melbourne.

The Widget will need to meet the following:
- Name of the selected city, Brisbane being the default

- Current temperature in the selected city

- An icon representing the weather condition in the city

- A dropdown menu which allows the user to change the selected city


## Project Setup

Setup your `.env` file by coping the contents of `.env.d.ts`

Uncomment `VITE_WEATHER_API_KEY` and input your openweather api key

```sh
npm install
```

### Compile and Hot-Reload for Development

```sh
npm run dev
```

### Type-Check, Compile and Minify for Production

```sh
npm run build
```

### Lint with [ESLint](https://eslint.org/)

```sh
npm run lint
```

## Addtional Information

With this task I allocated myself 3 hours as a time restraint, hour alotted for the previous task and then 3 for this for a total of 4 to keep it simple and focused.

I initally wanted to explore composition API, however, I was already struggling to remember bits and pieces of Vue so I decided not to try and implement it for this task as it might have posed too much of a distraction and loop trying to learn it while also re-learning vue basics.

Since it was a code challenge I opted to use hard values when it came to css such as 400px and so forth. I don't particularly like doing this and would prefer to have a pre-defined style and variables to make sure it is easier to have consistency in styling across the application.

If I had completed more than the above with time to spare, the next thing I would look to implement is testing, mainly starting with cypress, having it change values and recording changes in the city name and icon/temperature. However, I know this isn't as simple as it seems as there is a possibility the icon and temp could be the same which might break the test so would need to make sure it is not flaky. 

As stated from the above on not opting to use the composition API, this was also why I decided not to explore the optional parameter of geolocation. I have never really implemented something like this so it was going to be new terrority and I made the active choice to focus on the other criteria.

I also believe there is most likely a more eloquent solution to my dropdown and the switch selector used to change the temp and icon which I also would have liked to explore and breakdown with additional time, however, since it is a limited window (as in many other aspects) I went with bruteforce where I knew I could achieve the desired goal and then going back to refactor if time allowed.
