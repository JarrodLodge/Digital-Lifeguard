<template>
  <div class="container">
    <h4>Beach report for Omaha Beach</h4>
    <!-- SECTION 1 - Quick visual information -->
    <ul class="collection">
      <li class="collection-item">
        <div class="row">
          <div class="col s3">
            <i class="material-icons medium green-text sm3">pool</i>
          </div>
          <div class="col s9">
            <p>Always remember to swim between the flags</p>
          </div>
        </div>
      </li>
      <li class="collection-item">
        <div class="row">
          <div class="col s3">
            <i class="material-icons medium green-text">invert_colors</i>
          </div>
          <div class="col s9">
            <p>Water Quality:
              {{ waterRisk }}
            </p>
          </div>
        </div> 
      </li>
      <li class="collection-item">
        <div class="row">
          <div class="col s3">
            <i class="material-icons medium yellow-text">brightness_high</i>
          </div>
          <div class="col s9">
            <p>UV Burntime</p>
          </div>
        </div>
      </li>
    </ul>
    <!-- SECTION 2 - General Info -->
    <ul class="collection">
      <li class="collection-item">
        <div class="row">
          <div class="col s3">
            <i class="material-icons medium green-text sm3">flag</i>
          </div>
          <div class="col s9">
            <p>Patrol hours:
              10:30 am - 06:30pm
            </p>
          </div>
        </div>
      </li>
      <li class="collection-item">
        <div class="row">
          <div class="col s3">
            <i class="material-icons medium green-text">brightness_2</i>
          </div>
          <div class="col s9">
            <p>High Tides:
              {{ highTides[0] }}, {{ highTides[1] }}
            </p>
          </div>
        </div> 
      </li>
    </ul>
    <p>{{ surfData[0] }}</p>
  </div>
</template>

<script>
import db from './firebaseInit'
export default {
  data () {
    return {
      surfData: [],
      waterRisk: 'Low Risk',
      highTides: ['10:30am', '10:43pm']
    }
  },
  created () {
    db.collection('omaha').get()
      .then(querySnapshot => {
        querySnapshot.forEach(doc => {
          const data = {
            dt: doc.data().dt,
            description: doc.data().description,
            humidity: doc.data().humidity,
            pressure: doc.data().pressure,
            temp: doc.data().temp,
            windAngle: doc.data().windAngle,
            windSpeed: doc.data().windSpeed
          }
          this.surfData.push(data)
        })
      })
  }
}
</script>

