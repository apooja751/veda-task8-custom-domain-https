# Rollback Procedure

If the HTTPS configuration needs to be rolled back:

1. Open AWS EC2.
2. Open Load Balancers.
3. Select `veda-task8-alb`.
4. Open **Listeners and rules**.
5. Select the HTTP:80 listener.
6. Edit the default action.
7. Change the action from HTTPS redirect back to forwarding.
8. Select `veda-task8-tg`.
9. Save the changes.

The application can then be accessed through the original HTTP listener.

The HTTPS listener and ACM certificate can remain available or be removed according to the rollback requirement.
