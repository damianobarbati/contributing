# Environment variables

Environment variables are centralized in the root `.env`  
Available envs must be listed in the root `sample.env` file.  
Each service must have its `env.ts` responsible for reading, parsing and exporting 
the `process.env` as ENV object parsed with `zod`.  

NodeJS services read import and read the exported `ENV` object.  

If a new env is needed, the `sample.env` must be updated to reflect the change.

## NODE_ENV and APP_ENV

`NODE_ENV` variable indicates:
- `test`: the service is running in a test build.
- `development`: the service is running in a development build, where code is not minified nor optimized.
- `production`: the service is running in a production build, where code is minified and optimized.

Business logic must be agnostic to the `NODE_ENV` variable.  

`APP_ENV` variable indicates:
- `local`: the service is running on the developer's local machine.
- `development`: the service is running in `development` deployed environment.
- `staging`: the service is running in `staging` deployed environment.
- `production`: the service is running in `production` deployed environment.
