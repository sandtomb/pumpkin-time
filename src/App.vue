<template>
  <div id="pumpkin-competition-wrapper">
    <div id="title-wrapper">
      <h1>Pumpkin Carving Competition</h1>
    </div>
    <div>
      <h2>
        Current Pumpkin Count:
        {{ pumpkinContest.pumpkins.length }} / {{ pumpkinContest.MAX_PUMPKINS }}
      </h2>
    </div>
    <div id="state-display-wrapper">
      <div>
        <h4>
          Current State: 
        </h4>
      </div>
      <div id="current-state">
          {{ stateName }}
      </div>
      <svg v-if="stateName === 'Has Pumpkin'" width="100px" height="100px" viewBox="0 -74.5 1173 1173" class="icon"  version="1.1" xmlns="http://www.w3.org/2000/svg"><path d="M724.099 297.075c-44.381-67.192-84.69-112.825-106.859-125.736-4.987-2.903-15.845-9.228-30.376-9.069s-25.126 6.66-30.061 9.669c-21.875 13.342-60.827 58.923-103.302 125.661z" fill="#6BE166" /><path d="M656.488 272.001c11.668 0.883 26.978-15.32 27.241-30.45 0.736-42.993-119.948-79.702-123.525-72.832-2.051 3.883 36.616 15.299 64.982 58.554 15.835 24.147 18.981 43.792 31.302 44.727z" fill="#60C95B" /><path d="M453.492 318.633c-11.612-0.013-21.021-9.429-21.021-21.044 0-4.195 1.227-8.102 3.341-11.383 42.384-66.636 83.556-116.098 110.038-132.25 6.155-3.746 20.538-12.51 40.782-12.742s34.953 8.29 41.192 11.933c26.903 15.678 69.443 65.14 113.825 132.331 2.42 3.382 3.869 7.6 3.869 12.159 0 11.622-9.422 21.044-21.044 21.044-7.558 0-14.182-3.984-17.895-9.965-51.703-78.255-87.141-111.737-99.935-119.197-4.051-2.356-10.837-6.312-19.55-6.218s-15.352 4.209-19.329 6.587c-16.897 10.301-53.293 51.094-96.495 118.99-3.794 5.901-10.327 9.753-17.758 9.753-0.007 0-0.017 0-0.024 0z" fill="#000000" /><path d="M745.533 827.401c71.452-6.082 83.122 20.676 122.348 10.921 90.141-22.402 142.043-191.843 130.807-327.521-7.818-94.211-51.557-196.231-138.371-218.011-39.93-10.017-54.639 14.456-123.683 3.157-66.645-10.943-76.178-37.573-130.313-35.879-32.47 1.052-38.478 10.89-105.755 28.325-60.699 16.417-130.734 26.684-202.885 28.416 95.214-6.939 85.197-3.405 75.993 1.462-79.609 28.372-110.522 121.499-117.097 151.528-35.615 162.719 26.726 359.128 110.552 374.49 30.998 5.682 42.087-17.593 98.168-15.709 64.057 2.104 71.8 33.217 129.618 36.826 62.374 3.799 71.19-31.251 150.619-38.004z" fill="#EF863F" /><path d="M729.151 821.73c25.863 11.215 89.024 34.132 149.24 8.323 98.684-42.287 110.236-181.49 114.256-229.69 14.163-169.895-88.878-258.741-126.198-301.889-79.187-28.704-109.742-17.287-123.462-4.094-46.054 44.275 42.181 119.632 42.718 289.674 0.326 103.722-32.103 187.223-56.554 237.676z" fill="#CF7436" /><path d="M637.706 843.3c25.863-6.786 67.444-22.096 98.726-59.468 8.049-9.617 34.112-42.561 44.581-162.34 7.807-89.234 11.711-133.858-2.567-183.173-27.556-95.232-96.631-153.617-134.393-180.364 44.188 51.629 75.635 115.432 88.706 185.697 66.215 135.417-71.22 361.699-95.052 399.65z" fill="#CF7436" /><path d="M587.254 882.747c-34.090 0-53.661-8.418-72.599-16.54-16.75-7.197-32.617-13.994-61.804-16.668-35.647-3.262-55.008 2.873-73.736 8.817-17.077 5.419-34.721 11.017-58.637 6.187-23.411-4.734-45.643-17.887-66.076-39.088-18.202-18.877-34.438-43.582-48.326-73.452-1.239-2.603-1.963-5.654-1.963-8.875 0-11.622 9.422-21.044 21.045-21.044 8.402 0 15.653 4.924 19.027 12.042 23.507 50.57 54.347 83.018 84.65 89.152 13.215 2.672 22.906-0.401 37.563-5.050 20.58-6.523 46.191-14.647 90.298-10.607 35.879 3.283 56.439 12.121 74.579 19.907 17.14 7.364 30.66 13.173 56.323 13.12 25.474-0.053 38.877-5.85 55.838-13.184 18.003-7.785 38.415-16.614 74.157-19.991 44.192-4.209 69.864 3.757 90.487 10.185 14.73 4.578 24.463 7.608 37.71 4.902 23.147-4.714 46.159-24.011 66.666-55.819 23.947-37.152 42.151-88.245 51.251-143.874 9.701-59.301 8.481-118.433-3.515-171.021-3.924-17.212-28.083-104.859-117.97-139.36-7.423-2.83-16.009-4.673-24.961-5.122l13.283 1.744c-31.502-7.364-58.469 0.81-69.991 4.282l-2.504 0.747c-35.952 10.47-61.952-0.558-87.098-11.227-22.864-9.691-46.506-19.708-84.785-19.55-37.637 0.167-60.763 10.048-83.122 19.601-24.821 10.597-50.504 21.56-86.131 10.858l-2.736-0.841c-11.312-3.525-37.783-11.774-69.085-5.534l-0.653 0.116c-8.893 1.651-16.825 4.463-24.12 8.319-78.235 28.044-102.382 119.393-106.306 137.365-11.647 53.261-12.332 115.446-1.947 175.124 0.2 1.087 0.313 2.337 0.313 3.615 0 11.623-9.423 21.046-21.046 21.046-10.345 0-18.949-7.466-20.714-17.303-11.477-65.994-10.688-132.155 2.274-191.486 4.756-21.738 34.038-132.237 144.221-172.851 10.994-4.056 23.699-6.64 36.933-7.165 24.862-6.397 59.627 4.431 72.727 8.523l2.314 0.715c21.044 6.312 34.721 0.453 57.491-9.26 23.759-10.144 53.324-22.769 99.472-22.98 46.937-0.22 77.145 12.625 101.408 22.884 22.496 9.533 37.352 15.835 58.923 9.564l2.104-0.631c13.447-4.051 49.115-14.803 91.444-5.029 13.65 3.017 25.726 7.836 36.729 14.283 25.454 8.023 61.912 37.537 89.090 78.561 23.348 35.279 32.618 68.801 35.564 81.586 13.194 57.87 14.583 122.558 4.019 187.172-10.006 61.205-30.397 117.98-57.417 159.931-26.788 41.549-59.164 67.223-93.643 74.252-23.831 4.861-41.508-0.631-58.616-5.955-18.813-5.85-38.278-11.9-74-8.47-29.145 2.788-44.844 9.585-61.469 16.772-18.834 8.143-38.32 16.572-72.463 16.644z" fill="#000000" /><path d="M205.106 711.231c-9.436-0.003-17.421-6.215-20.089-14.772l-0.293-1.001c-0.618-1.892-0.975-4.070-0.975-6.33 0-11.622 9.422-21.044 21.044-21.044 9.543 0 17.604 6.353 20.181 15.061l0.27 0.907c0.58 1.835 0.914 3.946 0.914 6.135 0 11.622-9.422 21.044-21.044 21.044-0.004 0-0.007 0-0.008 0zM719.598 849.423c-11.618-0.007-21.035-9.425-21.035-21.044 0-3.33 0.773-6.479 2.15-9.277 39.936-81.133 63.434-176.715 63.697-277.76 0.797-109.222-28.852-167.754-52.632-214.786-3.63-7.165-7.060-13.942-10.322-20.749-1.319-2.673-2.091-5.819-2.091-9.146 0-11.622 9.422-21.044 21.044-21.044 8.334 0 15.537 4.844 18.945 11.872 3.117 6.521 6.452 13.099 9.967 20.053 24.504 48.4 58.080 114.687 57.186 238.097-0.978 107.827-26.632 209.437-71.577 299.757 0.198-0.773-6.978 4.027-15.274 4.027-0.021 0-0.042 0-0.064 0zM454.796 849.624c-0.002 0-0.005 0-0.007 0-8.359 0-15.578-4.872-18.974-11.933-41.713-86.488-66.069-187.915-66.1-295.030 0.106-121.567 32.154-184.583 57.975-235.202 3.62-7.102 7.039-13.805 10.185-20.349 3.622-6.656 10.566-11.098 18.546-11.098 11.622 0 21.044 9.422 21.044 21.044 0 3.003-0.629 5.859-1.763 8.444-3.304 6.842-6.829 13.744-10.553 21.067-23.779 46.622-53.24 104.606-53.346 216.58 0.096 100.582 23.024 195.783 63.878 280.737-0.598-1.654 0.147 1.441 0.147 4.709 0 11.618-9.414 21.037-21.032 21.044z" fill="#000000" /></svg>
      <svg v-else-if="stateName === 'Has Carved Pumpkin'" height="100px" width="100px" version="1.1" id="Layer_1" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" 
        viewBox="0 0 100 100" enable-background="new 0 0 100 100" xml:space="preserve">
      <g>
        <g>
          <path fill="#8BC53F" d="M47.6,23.7c0,0,0.7-6.7,2.8-6.7c2.2,0,2.5,7,2.5,7L47.6,23.7z"/>
        </g>
        <path fill="#231F20" d="M49.5,17c2.2,0,2.5,5,2.5,5l-5.3-0.3C46.6,21.7,47.3,17,49.5,17 M49.5,14c-3.5,0-5.3,3.7-5.8,7.2l-0.5,3.2
          l3.2,0.2l5.3,0.3l3.4,0.2l-0.2-3.4C54.7,18,53.1,14,49.5,14L49.5,14z"/>
        <g>
          <path fill="url(#SVGID_1_)" d="M83.6,50.8c0-13.4-8-24.3-17.9-24.3c-1.2,0-2.4,0.2-3.5,0.5c-2.8-2.6-6.1-4.1-9.6-4.1
            c-3.5,0-9.7,0.4-12.4,2.8c-0.9-0.2-0.2,0.5-1.2,0.5c-9.9,0-16.5,12.2-16.5,25.6c0,7.8,3.7,16.8,7.9,21.2c5.5,7.5,13,9.6,22.6,9.6
            S71.2,77.5,76.6,70C80.9,65.6,83.6,58.6,83.6,50.8z"/>
        </g>
        <g>
          <path fill="#231F20" d="M37.4,38.1c-0.1,0-0.3,0-0.4-0.1c-0.5-0.2-0.7-0.8-0.5-1.3c1.4-3,2.5-4.9,2.5-5c0.3-0.5,0.9-0.6,1.4-0.4
            c0.5,0.3,0.6,0.9,0.4,1.4c0,0-1.1,1.9-2.4,4.8C38.1,37.9,37.8,38.1,37.4,38.1z"/>
          <path fill="#231F20" d="M32.3,58.9c-0.5,0-1-0.4-1-1c0-0.3,0-0.7,0-1c0-3.1,0.5-6.6,1.6-10.4c0.1-0.5,0.7-0.8,1.2-0.7
            c0.5,0.1,0.8,0.7,0.7,1.2c-1,3.6-1.5,7-1.5,9.9c0,0.3,0,0.6,0,1C33.3,58.4,32.9,58.9,32.3,58.9C32.3,58.9,32.3,58.9,32.3,58.9z"/>
          <path fill="#231F20" d="M39.6,72.1c-0.2,0-0.3,0-0.5-0.1c-1.8-1-3.2-2.3-4.4-3.8c-0.3-0.4-0.3-1.1,0.2-1.4
            c0.4-0.3,1.1-0.3,1.4,0.2c1,1.3,2.3,2.4,3.8,3.3c0.5,0.3,0.6,0.9,0.4,1.4C40.2,72,39.9,72.1,39.6,72.1z"/>
        </g>
        <g>
          <path fill="#231F20" d="M60.8,38c-0.4,0-0.7-0.2-0.9-0.6c-1.4-2.9-2.5-4.7-2.5-4.8c-0.3-0.5-0.1-1.1,0.3-1.4
            c0.5-0.3,1.1-0.1,1.4,0.3c0,0.1,1.2,2,2.6,4.9c0.2,0.5,0,1.1-0.5,1.3C61.1,38,61,38,60.8,38z"/>
          <path fill="#231F20" d="M66.6,58.8C66.6,58.8,66.6,58.8,66.6,58.8c-0.6,0-1-0.5-1-1l0-0.2c0-3.1-0.6-6.7-1.8-10.7
            c-0.2-0.5,0.1-1.1,0.7-1.3c0.5-0.2,1.1,0.1,1.3,0.7c1.3,4.1,1.9,7.9,1.9,11.3l0,0.2C67.6,58.4,67.1,58.8,66.6,58.8z"/>
          <path fill="#231F20" d="M59.5,72.1c-0.3,0-0.7-0.2-0.9-0.5c-0.3-0.5-0.1-1.1,0.4-1.4c1.5-0.9,2.8-2,3.8-3.4c0.3-0.4,1-0.5,1.4-0.2
            c0.4,0.3,0.5,1,0.2,1.4C63.3,69.7,61.8,71,60,72C59.9,72.1,59.7,72.1,59.5,72.1z"/>
        </g>
        <path fill="#231F20" d="M48.9,23.7c3.3,0,6.5,1.5,9.1,3.9c1.1-0.3,2.2-0.4,3.3-0.4c9.4,0,16.9,10.5,16.9,23.5
          c0,7.5-2.6,14.2-6.5,18.5c-5.2,7.2-13.2,12.2-22.3,12.2s-17.2-5-22.3-12.2c-4-4.3-6.5-11-6.5-18.5c0-13,7.6-23.5,16.9-23.5
          c0.9,0,1.7,0.1,2.6,0.3C42.6,25,45.7,23.7,48.9,23.7 M48.9,20.7c-3.5,0-6.8,1.2-9.8,3.6c-0.6-0.1-1.1-0.1-1.7-0.1
          c-11,0-19.9,11.9-19.9,26.5c0,8,2.6,15.4,7.2,20.4c6,8.3,15.2,13.3,24.7,13.3S68,79.4,74,71.1c4.6-5,7.2-12.5,7.2-20.4
          c0-14.6-8.9-26.5-19.9-26.5c-0.8,0-1.6,0.1-2.4,0.2C55.9,21.9,52.4,20.7,48.9,20.7L48.9,20.7z"/>
        <g>
          <path fill="#FFF100" d="M40.8,47.4c-5,0-9-4-9-9c0-0.2,0-0.4,0-0.6c-2.6,1.6-4.3,4.4-4.3,7.7c0,5,4,9,9,9c4.8,0,8.7-3.7,9-8.5
            C44.1,46.9,42.5,47.4,40.8,47.4z"/>
          <path fill="#FFF100" d="M57.9,47.4c5,0,9-4,9-9c0-0.2,0-0.4,0-0.6c2.6,1.6,4.3,4.4,4.3,7.7c0,5-4,9-9,9c-4.8,0-8.7-3.7-9-8.5
            C54.6,46.9,56.2,47.4,57.9,47.4z"/>
        </g>
        <path fill="#FFF100" d="M49.4,68.3c-6.9,0-12.8-0.9-14.7-4.5c-0.4,0.8-0.7,1.7-0.7,2.6c0,4.9,6.9,9.8,15.4,9.8s15.4-4.9,15.4-9.8
          c0-0.9-0.2-1.8-0.7-2.6C62.2,67.4,56.3,68.3,49.4,68.3z"/>
        <g>
          <path fill="#231F20" d="M36.5,56C30.7,56,26,51.3,26,45.5c0-3.7,1.9-7.1,5.1-9c0.5-0.3,1.1-0.3,1.6,0c0.5,0.3,0.8,0.8,0.7,1.4
            l0,0.1c0,0.1,0,0.2,0,0.3c0,4.2,3.4,7.5,7.5,7.5c1.4,0,2.7-0.4,3.9-1.1c0.5-0.3,1.1-0.3,1.6,0c0.5,0.3,0.8,0.8,0.7,1.4
            C46.7,51.7,42,56,36.5,56z M30.6,40.8c-1,1.3-1.6,2.9-1.6,4.7c0,4.2,3.4,7.5,7.5,7.5c3,0,5.7-1.8,6.9-4.5
            c-0.8,0.2-1.7,0.3-2.6,0.3C35.9,48.9,31.7,45.4,30.6,40.8z"/>
          <path fill="#231F20" d="M62.2,56c-5.6,0-10.2-4.3-10.5-9.9c0-0.6,0.2-1.1,0.7-1.4c0.5-0.3,1.1-0.3,1.6,0c1.2,0.7,2.5,1.1,3.9,1.1
            c4.2,0,7.5-3.4,7.5-7.5c0-0.1,0-0.2,0-0.3l0-0.2c0-0.6,0.2-1.1,0.7-1.4c0.5-0.3,1.1-0.3,1.6,0c3.2,1.9,5.1,5.3,5.1,9
            C72.8,51.3,68,56,62.2,56z M55.4,48.6c1.2,2.6,3.8,4.5,6.9,4.5c4.2,0,7.5-3.4,7.5-7.5c0-1.7-0.6-3.4-1.6-4.7
            c-1.1,4.6-5.3,8-10.2,8C57,48.9,56.2,48.8,55.4,48.6z"/>
        </g>
        <path fill="#231F20" d="M63.5,64c0.4,0.8,0.7,1.6,0.7,2.5c0,4.7-6.6,9.4-14.8,9.4s-14.8-4.7-14.8-9.4c0-0.9,0.2-1.7,0.7-2.5
          c1.9,3.5,7.5,4.3,14.1,4.3S61.6,67.5,63.5,64 M63.5,61C63.5,61,63.5,61,63.5,61c-1.1,0-2.1,0.6-2.6,1.6c-0.7,1.2-3.2,2.7-11.5,2.7
          s-10.8-1.5-11.5-2.7c-0.5-1-1.5-1.6-2.6-1.6s-2.1,0.6-2.6,1.6c-0.7,1.3-1,2.6-1,3.9c0,6.7,8.2,12.4,17.8,12.4s17.8-5.7,17.8-12.4
          c0-1.4-0.3-2.7-1-3.9C65.6,61.7,64.6,61,63.5,61L63.5,61z"/>
      </g>
      </svg>
    </div>
    <div id="button-wrapper">
      <div id="eye-1" class="eye"></div>
      <div id="eye-2" class="eye"></div>
      <div id="eye-3" class="eye"></div>
      <div id="eye-4" class="eye"></div>
      <div id="eye-5" class="eye"></div>
      <div id="eye-6" class="eye"></div>
      <button
        id="pick-pumpkin"
        class="pumpkin-button"
        @click="pickPumpkin"
        >
        Pick Pumpkin
      </button>

      <button
        id="put-pumpkin-back"
        class="pumpkin-button"
        @click="putPumpkinBack"
        >
        Put Pumpkin Back
      </button>

      <button
        id="carve-pumpkin"
        class="pumpkin-button"
        @click="carvePumpkin"
        >
        Run Carve Pumpkin
      </button>

      <button
        id="submit-pumpkin"
        class="pumpkin-button"
        @click="submitPumpkin"
        >
          Submit Pumpkin
      </button>

      <button
        id="pick-winner"
        class="pumpkin-button"
        @click="pickWinner"
        >
          Pick Winner
      </button>
    </div>
  </div>
</template>

<script lang="ts">
import {
  ref,
  type Ref,
} from 'vue'

const POSSIBLE_PUMPKIN_DESIGNS = [
  'Ghost', 'Elf', 'Wizard', 'Archer', 'Knight', 'Pikachu', 'Eevee', 'Charmander', 'Scary Face', 'Happy Face', 'Sad Face'
]

class Pumpkin {
  id: string
  design: string

  constructor() {
    this.id = crypto.randomUUID()
    this.design = POSSIBLE_PUMPKIN_DESIGNS[(Math.floor(Math.random() * POSSIBLE_PUMPKIN_DESIGNS.length))]
  }

  toString(): string {
    return 'Pumpkin ID: ' + this.id + ' : with design: ' + this.design 
  }
}

interface State {
  name: string,
  pickPumpkin(): void,
  putPumpkinBack(): void,
  carvePumpkin(): void,
  submitPumpkin(): void,
}

class NoPumpkinState implements State {
  name: string
  pumpkinContest: PumpkinContest

  constructor(contest: PumpkinContest) {
    this.name = 'No Pumpkin'
    this.pumpkinContest = contest
  }

  pickPumpkin = (): void => {
    alert('You have picked a pumpkin')
    this.pumpkinContest.setState(this.pumpkinContest.getHasPumpkinState())
  }

  putPumpkinBack = (): void => {
    alert('You do not have a pumpkin to put back!')
  }

  carvePumpkin = (): void => {
    alert('You do not have a pumpkin to carve!')
  }

  submitPumpkin(): void {
    alert('You do not have have a pumpkin to submit!')
  }
}

class HasPumpkinState implements State {
  name: string
  pumpkinContest: PumpkinContest

  constructor(contest: PumpkinContest) {
    this.name = 'Has Pumpkin'
    this.pumpkinContest = contest
  }

  pickPumpkin = (): void => {
    alert('You already have a pumpkin')
  }

  putPumpkinBack = (): void => {
    alert('You put your pumpkin back into the patch')
    this.pumpkinContest.setState(this.pumpkinContest.getNoPumpkinState())
  }

  carvePumpkin = (): void => {
    alert('You carve your pumpkin!')
    this.pumpkinContest.setState(this.pumpkinContest.getCarvedPumpkinState())
  }

  submitPumpkin(): void {
    alert('You must have a carved pumpkin for an eligible submission!')
  }
}

class CarvedPumpkinState implements State {
  name: string
  pumpkinContest: PumpkinContest

  constructor(contest: PumpkinContest) {
    this.name = 'Has Carved Pumpkin'
    this.pumpkinContest = contest
  }

  pickPumpkin = (): void => {
    alert('You already have a pumpkin carved!')
  }

  putPumpkinBack = (): void => {
    alert('You would not want to put your already carved pumpkin back!')
  }

  carvePumpkin = (): void => {
    alert('You already carved your pumpkin!')
  }

  submitPumpkin(): void {
    const pumpkin: Pumpkin = new Pumpkin()
    this.pumpkinContest.addPumpkin(pumpkin)
    alert('You have successfully submitted your pumpkin: ' + pumpkin.toString())
    this.pumpkinContest.setState(this.pumpkinContest.getNoPumpkinState())
  }
}

type PumpkinContestState = (NoPumpkinState | HasPumpkinState | CarvedPumpkinState)

class PumpkinContest {
  MAX_PUMPKINS: number
  pumpkins: Array<Pumpkin>
  noPumpkinState: NoPumpkinState
  hasPumpkinState: HasPumpkinState
  carvedPumpkinState: CarvedPumpkinState
  state: PumpkinContestState

  constructor() {
    this.MAX_PUMPKINS = 5
    this.pumpkins = []
    this.noPumpkinState = new NoPumpkinState(this)
    this.hasPumpkinState = new HasPumpkinState(this)
    this.carvedPumpkinState = new CarvedPumpkinState(this)
    this.state = this.noPumpkinState
  }

  getNoPumpkinState = (): PumpkinContestState => {
    return this.noPumpkinState
  }

  getHasPumpkinState = (): PumpkinContestState => {
    return this.hasPumpkinState
  }

  getCarvedPumpkinState = (): PumpkinContestState => {
    return this.carvedPumpkinState
  }

  setState = (newState: PumpkinContestState): void => {
    this.state = newState
  }

  pickPumpkin = (): void => {
    this.state.pickPumpkin()
  }

  putPumpkinBack = (): void => {
    this.state.putPumpkinBack()
  }

  carvePumpkin = (): void => {
    this.state.carvePumpkin()
  }

  submitPumpkin(): void {
    if (this.isFull()) {
      alert('Carving Competition is full - Time to select a winner!')
    } else {
      this.state.submitPumpkin()
    }
  }

  addPumpkin(pumpkin: Pumpkin): void {
    this.pumpkins.push(pumpkin)
  }

  clearPumpkins(): void {
    this.pumpkins = []
  }

  isFull(): boolean {
    return this.pumpkins.length >= this.MAX_PUMPKINS
  }

  pickWinner() : void {
    if (this.pumpkins.length >= this.MAX_PUMPKINS) {
      const winner: Pumpkin = this.pumpkins[(Math.floor(Math.random() * this.pumpkins.length))]
      this.pumpkins = []
      this.setState(this.getNoPumpkinState())
      alert('Winner is: ' + winner.toString())
    } else {
      alert('Not enough pumpkins have been submitted!')
    }
  }
}

export default {
  setup() {
    const pumpkinContest:Ref<PumpkinContest> = ref(new PumpkinContest())
    const stateName: Ref<string> = ref(pumpkinContest.value.state.name)

    const pickPumpkin = (): void => {
      pumpkinContest.value.pickPumpkin()
      stateName.value = pumpkinContest.value.state.name
    }

    const putPumpkinBack = (): void => {
      pumpkinContest.value.putPumpkinBack()
      stateName.value = pumpkinContest.value.state.name
    }

    const carvePumpkin = (): void => {
      pumpkinContest.value.carvePumpkin()
      stateName.value = pumpkinContest.value.state.name
    }

    const submitPumpkin = (): void => {
      pumpkinContest.value.submitPumpkin()
      stateName.value = pumpkinContest.value.state.name
    }

    const pickWinner = (): void => {
      pumpkinContest.value.pickWinner()
      stateName.value = pumpkinContest.value.state.name
    }

    return {
      pumpkinContest,
      stateName,
      pickPumpkin,
      putPumpkinBack,
      carvePumpkin,
      submitPumpkin,
      pickWinner,
    }
  }
}

</script>

<style scoped>
  .a{fill:#f4b467;}.b{fill:#a98a75;}.c{fill:#211715;}.d{fill:#ffffff;}

  #pumpkin-competition-wrapper{
    display: flex;
    height: 100vh;
    width: 100%;
    flex-direction: column;
    align-items: center;
    justify-content: space-around;
    padding: 0;

    position: relative;
    width: 100%;
    height: 100vh;
    background-color: #4a4a4a; /* Dark background */
    overflow: hidden;
  }

  @keyframes blink {
    0%{
      opacity: 0;
    }
    75% {
      opacity: 0;
    }
    100% {
      opacity: 50%;
    }
  }

  .eye {
    position: absolute;
    width: 30px;
    height: 50px;
    background-color: rgba(255, 255, 255, 0.129);
    border-radius: 100%;
    margin: auto;
  }

  #eye-1 {
    left: 25%;
    top: 85%;
    animation: blink 15s infinite;
  }

  #eye-2 {
    left: 65%;
    top: 85%;
    animation: blink 15s infinite;
  }

  #eye-3 {
    left: 90%;
    top: 15%;
    opacity: 20%;
    animation: blink 5s infinite;
  }

  #eye-4 {
    left: 15%;
    top: 65%;
    opacity: 20%;
    animation: blink 14s infinite;
  }

  #eye-5 {
    left: 5%;
    top: 77%;
    opacity: 20%;
    animation: blink 8s infinite;
  }

  #eye-6 {
    left: 75%;
    top: 85%;
    opacity: 20%;
    animation: blink 7s infinite;
  }

  .eye::before {
    content: '';
    position: absolute;
    top: 10px;
    left: 5px;
    width: 10px;
    height: 30px;
    background-color: #000;
    border-radius: 50%;
  }

  .pumpkin-button {
    height: 4em;
    margin: .2em;
    background-color: #e67e22; /* Pumpkin orange */
    border: 2px solid #544e4e; /* Dark border for contrast */
    color: #fff; /* White text for readability */
    font-weight: bold;
    border-radius: 4em; /* Rounded corners */
    cursor: pointer;
    transition: all 0.3s ease; /* Smooth transition for button press effect */
  }

  #state-display-wrapper {
    display: flex;
    align-items: center;
    justify-content: center;
    text-align: center;
  }

  .pumpkin-button:hover {
    background-color: #d35400; /* A darker orange on hover */
  }

  .pumpkin-button:active {
    box-shadow: 0 1px #666; /* Less shadow to simulate button press */
    transform: translateY(3px); /* Move the button down to simulate press */
  }

  /* Optional: A stem-like element for the button */
  .pumpkin-button::before {
    content: "";
    display: block;
    position: absolute;
    top: -16px;
    left: 50%;
    transform: translateX(-50%);
    width: 6px;
    height: 16px;
    background-color: #27ae60; /* Color of the stem */
    border-radius: 50%;
  }

  #button-wrapper {
    display: flex;
    justify-content: center;
  }

  #title-wrapper {
    display: flex;
    justify-content: center;
  }

  #current-state {
    position: relative;
    color: white;
    display: flex;
    justify-content: center;
    align-items: center;
    min-width: 4em;
    text-align: center;
    height: 2em;
    padding: .4em;
    border: .2em solid transparent; /* Make border transparent initially */
    border-radius: 2em;
    margin-left: .2em;
    overflow: hidden; /* Ensure the pseudo-element does not extend outside */
  }

  @keyframes trace-border {
  0% {
    box-shadow: inset 0 0 0 0 #d35400;
  }
  80% {
    box-shadow: inset 0 0 0 .1em #d35400;
  }
  100% {
    box-shadow: inset 0 0 0 .2em #d35400;
  }
}

#current-state::before {
  content: '';
  position: absolute;
  top: 0;
  right: 0;
  bottom: 0;
  left: 0;
  border-radius: inherit; /* Use the same border-radius as the parent */
  animation: trace-border 5s infinite; /* Adjust the timing as needed */
}

</style>
