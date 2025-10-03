---
title: "Taskflow"
date: 2025-10-03
draft: false
categories: ["Web Development", "DevOps"]
tags: ["CI/CD", "Vercel"]
description: "To-Do app using CI/CD pipeline"
---

{{< timeline >}}

{{< timelineItem icon="code" header="The Blueprint" badge="">}}
The goal was to create a sleek, cyberpunk-themed To-Do application that was both functional and stylish. The project, TaskFlow, started with a solid, modern tech stack.

The backend was built on <b>Node.js</b> and <b>Express</b>, handling user authentication with JWTs and task management. For the database, I initially chose <b>Prisma</b> as the ORM to simplify interactions with a PostgreSQL database. The frontend was crafted with vanilla <b>HTML, CSS, and JavaScript</b>, using the Tailwind CSS CDN for rapid, futuristic styling. This initial setup provided a full-featured application with secure user accounts and full CRUD (Create, Read, Update, Delete) functionality for tasks.
{{< /timelineItem >}}

{{< timelineItem icon="pencil" header="Going Prisma-less" badge="">}}
While Prisma was powerful, I wanted to get closer to the database and write raw SQL for more control and a better understanding of the underlying operations. This led to a major refactor of the backend.

I removed Prisma and integrated the <code>pg</code> library to communicate directly with the PostgreSQL database. This meant rewriting every database query by hand, which was a fantastic learning experience. It also introduced a new challenge: <b>database migrations</b>. Without Prisma's <code>migrate</code> command, I had to learn how to manually create and manage the database schema, leading to my first run-in with the infamous <code>relation "Todo" does not exist</code> error 😅.
{{< /timelineItem >}}

{{< timelineItem icon="shield" header="Containerization & CI/CD" badge="">}}
With the application logic solidified, the next goal was to make it portable and easy to deploy. This was the perfect job for <b>Docker</b>. I wrote a <code>Dockerfile</code> to create a self-contained, reproducible image of the application.

To automate the build process, I set up a CI/CD pipeline using <b>GitHub Actions</b>. Every push to the <code>main</code> branch would automatically trigger a workflow to build the Docker image and push it to <b>Docker Hub</b>. This ensured that a tested, ready-to-deploy version of the app was always available.

{{< mermaid >}}
graph TD;
    A[Git Push to Main] --> B{GitHub Actions};
    B --> C[Build Docker Image];
    C --> D[Push Image to Docker Hub];
{{< /mermaid >}}
{{< /timelineItem >}}

{{< timelineItem icon="globe" header="Launch on Vercel" badge="">}}
The final step was deployment. I chose <b>Vercel</b> for its seamless Git integration and generous free tier. The initial plan to deploy the pre-built image from Docker Hub hit a snag, as Vercel's UI had changed to prioritize a Git-based workflow.

I pivoted to connecting the GitHub repository directly to Vercel. Vercel automatically detected the <code>Dockerfile</code>, built the image, and deployed the container. The last piece of the puzzle was setting up the production database using <b>Vercel Postgres</b>. I connected to it, manually ran the SQL script to create the <code>User</code> and <code>Todo</code> tables, and the site was live! Post-launch, I added a few quality-of-life improvements, like adding a "briefing" field for tasks and fixing the initial page "flash" for a smoother user experience.
{{< /timelineItem >}}

{{< /timeline >}}

This timeline covers the high-level journey of building and deploying TaskFlow. Along the way, I learned a ton about the nuances of raw SQL with `node-pg`, the best practices for writing a `Dockerfile`, and the intricacies of deploying a containerized application on Vercel.

{{< button href="[https://task-flow-dun-beta.vercel.app/](https://task-flow-dun-beta.vercel.app/)" target="_blank" >}} TaskFlow Live {{< /button >}}
{{< github repo="a-p-n/Taskflow" >}}
