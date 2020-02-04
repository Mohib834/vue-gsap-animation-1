<template>
  <nav>
    <h3>Logo</h3>
    <ul>
      <li>About us</li>
      <li>/</li>
      <li>
        <strong>Menu</strong>
      </li>
      <li @click="$emit('initiateAnimation')">Start</li>
    </ul>
  </nav>
</template>