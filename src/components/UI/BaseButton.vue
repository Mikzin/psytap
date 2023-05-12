<template>
  <button class="button">
    <slot></slot>
  </button>
</template>

<style scoped>
.button {
  font-size: 16px;
  background-color: #8294c4;
  color: #dbdfea;
  width: 60%;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  border-radius: 24px;
  padding: 12px 8px;
  cursor: pointer;
  margin: 8px;
  font-weight: bold;
  border: none;
}

.button:hover {
  background-color: #acb1d6;
}

@media screen and (max-width: 500px) {
  .button {
    padding: 16px 8px;
    width: 80%;
  }
}
</style>
