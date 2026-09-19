<p align="center">
  <img src="assets/logo.png" alt="KeyTask" width="110" /> 
</p>

# KeyTask

A task manager for teams, with the login handled by Keycloak instead of by the app.

I built this during a one-month internship at Lunar TC. The tasks and groups are
straightforward; the point of the project was learning how single sign-on actually
works — letting Keycloak own identity and having the API just validate the token it
issues.

| Landing page | Keycloak login |
| :---: | :---: |
| ![Landing page](assets/welcome.png) | ![Keycloak login](assets/keycloak-login.png) |

## What it does

- Create a group, join one, manage its members
- Assign tasks that repeat daily, weekly, monthly or yearly
- Sign in once through Keycloak (OAuth2 / OIDC) — no passwords stored in the app
- Restrict admin actions by role

**Built with** Spring Boot 3, Angular 19, MongoDB and Keycloak 26.

## Running it

You'll need JDK 23, Node 18+, and Docker for the services.

```bash
docker run -d -p 27017:27017 mongo:6
docker run -d -p 8080:8080 \
  -e KEYCLOAK_ADMIN=admin -e KEYCLOAK_ADMIN_PASSWORD=admin \
  quay.io/keycloak/keycloak:26.0 start-dev
```

In the Keycloak console at `localhost:8080`, create a realm called **KeyTask** and a
public client allowing `http://localhost:4200/*`.

```bash
git clone https://github.com/salmenhammami/KeyTask.git

cd KeyTask/Projet/Backend
./mvnw spring-boot:run        # Windows: mvnw.cmd spring-boot:run

cd ../Frontend
npm install && npm start
```

The API runs on port 8081, the Angular app on 4200.

## Honest notes

This was early-internship work. The realm has to be set up by hand because I never
exported it, the issuer URI in `application.yml` is nested under the wrong key so
Spring doesn't pick it up, and there are no tests yet. All three are on my list.

---

**Salmen Hammami** · [GitHub](https://github.com/salmenhammami) · [LinkedIn](https://www.linkedin.com/in/salmenhammami/)
