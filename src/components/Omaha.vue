<template>
  <div class="container">
    <div class="row">
      <a href="tel:0800728354837"
        class="left waves-effect waves-light btn red yellow-text text-accent-2"
        style="margin-top:1em">GET HELP NOW!</a>
      <h5 class="right" style="margin-top:1em">Omaha Beach</h5>
    </div>
    <!-- SECTION 1 - Quick visual information -->
    <ul class="collection" style="border: 0!important">
      <li class="collection-item" style="border: 0!important">
        <div class="row">
          <div class="col s3">
            <i class="material-icons medium green-text sm3">pool</i>
          </div>
          <div class="col s9">
            <p>{{ surfData[0].surfMessage }}</p>
          </div>
        </div>
      </li>
      <li class="collection-item" style="border: 0!important">
        <div class="row">
          <div class="col s3">
            <i class="material-icons medium green-text">invert_colors</i>
          </div>
          <div class="col s9">
            <p>Water Quality:
              {{ surfData[0].waterRisk }}
            </p>
          </div>
        </div> 
      </li>
      <li class="collection-item">
        <div class="row">
          <div class="col s3">
            <i class="material-icons medium red-text">brightness_high</i>
          </div>
          <div class="col s9">
            <p>UV Index: {{ surfData[0].uvIndex }}</p>
          </div>
        </div>
      </li>
    </ul>
    <!-- SECTION 2 - General Info -->
    <ul class="collection" style="border: 0!important">
      <li class="collection-item" style="border: 0!important">
        <div class="row">
          <div class="col s3">
            <i class="material-icons medium green-text sm3">flag</i>
          </div>
          <div class="col s9">
            <div>
              Patrol hours:
            </div>
            <div>
              10:30 am - 06:30pm
            </div>            
          </div>
        </div>
      </li>
      <li class="collection-item" style="border: 0!important">
        <div class="row">
          <div class="col s3">
            <i class="material-icons medium green-text">brightness_2</i>
          </div>
          <div class="col s9">
            <div>High Tides:</div>
            <div>{{ surfData[0].highTides[0] }}, {{ surfData[0].highTides[1] }}</div>
          </div>
        </div> 
      </li>
    </ul>
    <!-- Feed back button to form -->
    <div>
      <a href="mailto:adam.wooler@lifesaving.org.nz?Subject=Hazard%20at%20Omaha%20Beach"
        class="waves-effect waves-light btn red yellow-text text-accent-2"
        style="margin-top:1em">REPORT A HAZARD!</a>
    </div>
    <!-- Beach Information -->
    <div class="row">
        <div class="col s12 m7">
          <div class="card">
            <div class="card-image">
              <img src="https://c1.staticflickr.com/3/2849/12244578143_00eff1a1b7_b.jpg">
              <span class="card-title">About Omaha Beach</span>
            </div>
            <div class="card-content">
              <p>Omaha Beach is a great place to spend the day with family and friends. Go for a walk, swim, or head out on paddle craft. Swimmers should make sure they stay within their limits, swim between the red and yellow flags, and keep young children within arm's reach. The beach can get good surf, but be aware that the waves may dump during outgoing tides, and rip currents are common along the beach. If you're planning on taking paddle craft out, stay clear of the red and yellow flags and be mindful of other water users. Also, make sure you check the conditions first, especially the wind as it may be stronger than it appears.
              </p>
              <p>
              Long-term monitoring by Auckland Council at Omaha has consistently identified good water quality. However, please exercise caution following heavy rain in this area.</p>
            </div>
            <div class="card-action">
              <a href="https://safeswim.org.nz">Visit Safeswim to find out more about water quality</a>
            </div>
          </div>
        </div>
      </div>
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
            dt: doc.data().dt.toLocaleString(),
            description: doc.data().description,
            humidity: doc.data().humidity,
            pressure: doc.data().pressure,
            temp: doc.data().temp,
            windAngle: doc.data().windAngle,
            windSpeed: doc.data().windSpeed,
            highTides: doc.data().highTides,
            waterRisk: doc.data().waterRisk,
            surfMessage: doc.data().surfMessage,
            uvIndex: doc.data().uvIndex
          }
          this.surfData.push(data)
        })
      })
  }
}
</script>

