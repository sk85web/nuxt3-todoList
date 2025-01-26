<template>
  <NuxtPage />
</template>

<style>
body {
  font-family: 'Montserrat', sans-serif;
  font-size: 14px;
}

button {
  font-family: inherit;
  border-radius: 5px;
  cursor: pointer;
  transition: all 0.2s linear;
  font-weight: normal;
}

button:hover {
  background-color: rgb(96, 225, 242);
}

.container {
  max-width: 320px;
  display: flex;
  flex-direction: column;
  justify-content: center;
  height: auto;
  width: 100%;
  margin: 0 auto;
  padding: 1rem;
  background: #211f2d;
  border-radius: 10px;
}

.title {
  text-align: center;
  color: rgb(96, 225, 242);
}

a {
  color: #fff;
  text-decoration: none;
  transition: all 0.2s linear;
}
</style>
