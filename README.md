# Blazor ClientWasm and SSR Auth App Example

A .NET 10 Blazor Web App that demonstrates authentication and authorization using **ASP.NET Core Identity cookies** with interactive WebAssembly components.

## Authenticated experience

<img width="804" height="515" alt="image" src="https://github.com/user-attachments/assets/433032e5-b179-413c-ad4a-49709beccabb" />

The screenshot shows a signed-in user accessing a protected page (`/auth`) and viewing server-protected data.

## How authentication and authorization work

This app follows the Blazor security model described in Microsoft docs:
- https://learn.microsoft.com/en-us/aspnet/core/blazor/security/?view=aspnetcore-10.0&tabs=visual-studio

### Authentication (Identity cookie)

1. A user signs in through ASP.NET Core Identity endpoints.
2. The server issues an authentication cookie.
3. On subsequent requests, the cookie identifies the user to the server.
4. Blazor uses the authenticated `HttpContext.User` to build the app auth state.

### Authorization (protected UI + protected data)

- UI access is controlled with Blazor authorization primitives such as `[Authorize]`, `AuthorizeRouteView`, and `AuthorizeView`.
- Server endpoints must also enforce authorization (for example with `.RequireAuthorization()`), so protected data stays secure even when components run interactively.

### Blazor Web App + WebAssembly behavior

In interactive WebAssembly/Auto scenarios, authentication is still server-driven:
- The server authenticates users with Identity cookies.
- Auth state is serialized/deserialized for the client experience.
- Actual server data protection remains enforced on server endpoints and policies.

## Run locally

1. Restore and build.
2. Run the server project.
3. Register/sign in with a local account.
4. Navigate to `/auth` to verify protected content is available only to authenticated users.
