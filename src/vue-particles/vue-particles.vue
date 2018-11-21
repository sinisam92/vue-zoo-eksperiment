<template>
  <div
    class="particles-js"
    :id="id"
    :color="color"
    :particleOpacity="particleOpacity"
    :linesColor="linesColor"
    :particlesNumber="particlesNumber"
    :shapeType="shapeType"
    :particleSize="particleSize"
    :linesWidth="linesWidth"
    :lineLinked="lineLinked"
    :lineOpacity="lineOpacity"
    :linesDistance="linesDistance"
    :moveSpeed="moveSpeed"
    :hoverEffect="hoverEffect"
    :hoverMode="hoverMode"
    :clickEffect="clickEffect"
    :clickMode="clickMode"
  >
  <div class="moj-div">
        <form @submit.prevent="addAnimal" class="form-group">
            
            <input v-model="newAnimal.spicies" placeholder="Spicies">
            
            <input v-model="newAnimal.name" placeholder="Name">
            
            <input v-model="newAnimal.dateOfBirth" placeholder="Date Of Birth">

            <select v-model="newAnimal.sector" aria-placeholder="Select Section">
                <option disabled value="">Please select one</option>
                <option v-for="(sector, index) in sectors" :key="index" :value="sector">{{sector.name}}</option>
            </select>
            
            <button type="submit" class="btn btn-primary">Add Animal</button><br>
        </form>
       <h1>Sve zivotinje</h1>
       <div class="table-container">
         <div class="table1-container">
            <table border="2">
            <thead>
                <td>Spicies</td>
                <td>Name</td>
                <td>Date Of Birth</td>
                <td>Sector</td>
                
            </thead>
            <tbody>
                <tr v-for="(animal, index) in animals" :key="index">
                    <td>{{animal.spicies}}</td>
                    <td>{{animal.name}}</td>
                    <td>{{animal.dateOfBirth ? animal.dateOfBirth : 'Nepoznat'}}</td>
                    <!-- <td v-if="animal.dateOfBirth">{{animal.dateOfBirth}}</td>
                    <td v-if="!animal.dateOfBirth">'Nepoznat'</td> -->
                    <td>{{animal.sector.name}}</td>
                    <td>
                    <button @click="removeAnimal(animal)" type="submit" class="btn btn-primary">Remove</button>
                    </td>
                    <td>
                    <button @click="moveToTop(animal)" type="submit" class="btn btn-primary">Move to top</button>
                    </td>
                </tr>
            </tbody>
        </table>
         </div>
         
        <div class="table2-container">
            <table border="2">
            <thead>
                <td>Name</td>
                <td>Surface</td>
            </thead>
            <tbody>
                <tr v-for="(sector, index) in sectors" :key="index">
                    <td>{{sector.name}}</td>
                    <td>{{sector.surface}}</td>
                    <td>
                        <button @click="showAnimals(sector)" type="submit" class="btn btn-primary">Vidi Zivotinje</button>
                    </td>
                </tr>
            </tbody>
        </table>
        </div>
       </div>
      </div>
        
    </div>
    
</template>
<script>
const sectors = [
    {name: 'Water-animals', surface: 'Water'},
    {name: 'Air-animals', surface: 'Air'},
    {name: 'Dinosaurusi', surface: 'All-around'}
]
  /* eslint-disable */
  export default {
    name: 'vue-particles',
    data: function () {
      return {
        id: 'particles-instance-' + Math.floor(Math.random() * 5000),
        sectors: sectors,
            newAnimal: {},
            animals: [
                {spicies: 'Sisar', name: 'Spajk', dateOfBirth: '10 05 2006', sector:sectors[0]},
                {spicies: 'Glodar', name: 'Misko', dateOfBirth: '11 06 2007', sector:sectors[1]},
                {spicies: 'Vodozemac', name: 'Zabra', dateOfBirth: '12 07 2007', sector:sectors[0]},
                {spicies: 'Dinosaurus', name: 'Perodaktil', dateOfBirth: '10 05 2006', sector:sectors[2]},
                {spicies: 'Sisar', name: 'Sinisa', dateOfBirth: '16 08 2016', sector:sectors[1]},
                {spicies: 'Komsija', name: 'Dejan', dateOfBirth: '', sector:sectors[0]}
            ]
            
      }
    },
    props: {
      color: {
        type: String,
        default: '#dedede'
      },
      particleOpacity: {
        type: Number,
        default: 0.7
      },
      particlesNumber: {
        type: Number,
        default: 80
      },
      shapeType: {
        type: String,
        default: 'circle'
      },
      particleSize: {
        type: Number,
        default: 4
      },
      linesColor: {
        type: String,
        default: '#dedede'
      },
      linesWidth: {
        type: Number,
        default: 1
      },
      lineLinked: {
        type: Boolean,
        default: true
      },
      lineOpacity: {
        type: Number,
        default: 0.4
      },
      linesDistance: {
        type: Number,
        default: 150
      },
      moveSpeed: {
        type: Number,
        default: 3
      },
      hoverEffect: {
        type: Boolean,
        default: true
      },
      hoverMode: {
        type: String,
        default: 'grab'
      },
      clickEffect: {
        type: Boolean,
        default: true
      },
      clickMode: {
        type: String,
        default: 'push'
      }
    },
    mounted () {
      // import particle.js only on client-side
      require('particles.js')
      this.$nextTick(() => {
        this.initParticleJS(
          this.color,
          this.particleOpacity,
          this.particlesNumber,
          this.shapeType,
          this.particleSize,
          this.linesColor,
          this.linesWidth,
          this.lineLinked,
          this.lineOpacity,
          this.linesDistance,
          this.moveSpeed,
          this.hoverEffect,
          this.hoverMode,
          this.clickEffect,
          this.clickMode
        )
      })
    },
    methods: {
      initParticleJS (
        color,
        particleOpacity,
        particlesNumber,
        shapeType,
        particleSize,
        linesColor,
        linesWidth,
        lineLinked,
        lineOpacity,
        linesDistance,
        moveSpeed,
        hoverEffect,
        hoverMode,
        clickEffect,
        clickMode
      ) {
        particlesJS(this.id, {
          "particles": {
            "number": {
              "value": particlesNumber,
              "density": {
                "enable": true,
                "value_area": 800
              }
            },
            "color": {
              "value": color
            },
            "shape": {
              // circle, edge, triangle, polygon, star, image
              "type": shapeType,
              "stroke": {
                "width": 0,
                "color": "#192231"
              },
              "polygon": {
                "nb_sides": 5
              }
            },
            "opacity": {
              "value": particleOpacity,
              "random": false,
              "anim": {
                "enable": false,
                "speed": 1,
                "opacity_min": 0.1,
                "sync": false
              }
            },
            "size": {
              "value": particleSize,
              "random": true,
              "anim": {
                "enable": false,
                "speed": 40,
                "size_min": 0.1,
                "sync": false
              }
            },
            "line_linked": {
              "enable": lineLinked,
              "distance": linesDistance,
              "color": linesColor,
              "opacity": lineOpacity,
              "width": linesWidth
            },
            "move": {
              "enable": true,
              "speed": moveSpeed,
              "direction": "none",
              "random": false,
              "straight": false,
              "out_mode": "out",
              "bounce": false,
              "attract": {
                "enable": false,
                "rotateX": 600,
                "rotateY": 1200
              }
            }
          },
          "interactivity": {
            "detect_on": "canvas",
            "events": {
              "onhover": {
                "enable": hoverEffect,
                "mode": hoverMode
              },
              "onclick": {
                "enable": clickEffect,
                "mode": clickMode
              },
              "onresize": {

                "enable": true,
                "density_auto": true,
                "density_area": 400

              }
            },
            "modes": {
              "grab": {
                "distance": 140,
                "line_linked": {
                  "opacity": 1
                }
              },
              "bubble": {
                "distance": 400,
                "size": 40,
                "duration": 2,
                "opacity": 8,
                "speed": 3
              },
              "repulse": {
                "distance": 200,
                "duration": 0.4
              },
              "push": {
                "particles_nb": 4
              },
              "remove": {
                "particles_nb": 2
              }
            }
          },
          "retina_detect": true
        });
      },
      removeAnimal(animal) {
            let index = this.animals.indexOf(animal);
            this.animals.splice(index, 1);
        },
        moveToTop(animal) {
            let index = this.animals.indexOf(animal);
            this.animals.splice(index, 1);
            this.animals.unshift(animal);
        },
        addAnimal() {
            console.log(this.newAnimal);
            
            this.animals.push(this.newAnimal);
            this.newAnimal = {dateOfBirth: ''};
        },
        showAnimals(sector) {
            let animals = [];
           this.animals.forEach((currentAnimal) => {
            if(currentAnimal.sector == sector){

                    animals.push(currentAnimal.name);  
               }    
                
           });
           alert(animals);  
          
        }

    }
  }
  /* eslint-disable */
</script>

<style scoped>
h3 {
  margin: 40px 0 0;
}
.main-container {
    padding-top: 1rem;
}
.btn {
    margin: 1rem;
    color: rgb(12, 11, 11);
    background-color: #fff;
}
.table2-container {
    margin-left: 40px;
}
input {
    border-radius: 10px;
}
table {
  color: white;
  font-weight: 600;
  border: 5px;
  border-radius: 5px; 
  border-color: white;
}
.moj-div{
  margin-left: 5%;
  position: absolute;
  color: #fff;
  font-family: sans-serif;
  
}
.moj-div h1 {
  font-size: 60px;
  text-shadow: 8px 8px #000;
}
.table-container {
  display: flex;
  justify-content: space-between;
}
select {
  margin-left: 5px;
}

</style>
