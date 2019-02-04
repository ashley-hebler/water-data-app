<template>
  <div>
    <nav class="navbar has-background-white-ter" role="navigation" aria-label="main navigation">
      <div class="navbar-brand">
        <a class="navbar-item" href="/">
          <svg fill="#2c8ef3" xmlns="http://www.w3.org/2000/svg" width="50" height="50" viewBox="0 0 24 24">
            <path
              d="M18.356 10.123l-1.855.783c-.485-.976-1.08-2.017-1.769-3.133l1.555-1.296c.811 1.3 1.508 2.507 2.069 3.646zm-13.583 2.02c-.5 1.363-.773 2.654-.773 3.932l.016.312 1.987-.349c.005-.979.237-2.011.63-3.109l-1.86-.786zm15.227 3.932c0-1.278-.273-2.569-.773-3.932l-1.859.786c.393 1.099.625 2.131.63 3.109l1.987.349.015-.312zm-14.356-5.952l1.855.783c.485-.976 1.08-2.018 1.769-3.133l-1.555-1.296c-.811 1.3-1.508 2.507-2.069 3.646zm8.126 11.613c-.56.171-1.155.264-1.77.264s-1.21-.093-1.77-.264l-.999 1.767c.865.316 1.794.497 2.769.497s1.904-.181 2.769-.497l-.999-1.767zm-3.313-15.836c.486-.745.994-1.513 1.543-2.329.549.816 1.057 1.583 1.543 2.329l1.549-1.291c-.926-1.414-1.959-2.936-3.092-4.609-1.133 1.673-2.166 3.195-3.092 4.609l1.549 1.291zm7.137 12.301c-.39.996-1.041 1.861-1.874 2.514l.991 1.755c1.336-.967 2.357-2.329 2.885-3.917l-2.002-.352zm-9.314 2.514c-.833-.653-1.484-1.519-1.874-2.514l-2.002.352c.527 1.588 1.549 2.951 2.885 3.917l.991-1.755z"
            />
          </svg>
          <span class="is-size-2 is-family-secondary">Water Stats</span>
        </a>
      </div>
    </nav>
    <nuxt/>
  </div>
</template>

<style>
html {
  font-family: 'Source Sans Pro', -apple-system, BlinkMacSystemFont, 'Segoe UI',
    Roboto, 'Helvetica Neue', Arial, sans-serif;
  font-size: 16px;
  word-spacing: 1px;
  -ms-text-size-adjust: 100%;
  -webkit-text-size-adjust: 100%;
  -moz-osx-font-smoothing: grayscale;
  -webkit-font-smoothing: antialiased;
  box-sizing: border-box;
}

*,
*:before,
*:after {
  box-sizing: border-box;
  margin: 0;
}

.button--green {
  display: inline-block;
  border-radius: 4px;
  border: 1px solid #3b8070;
  color: #3b8070;
  text-decoration: none;
  padding: 10px 30px;
}

.button--green:hover {
  color: #fff;
  background-color: #3b8070;
}

.button--grey {
  display: inline-block;
  border-radius: 4px;
  border: 1px solid #35495e;
  color: #35495e;
  text-decoration: none;
  padding: 10px 30px;
  margin-left: 15px;
}

.button--grey:hover {
  color: #fff;
  background-color: #35495e;
}
</style>
