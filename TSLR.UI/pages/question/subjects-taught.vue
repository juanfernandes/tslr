<template>
  <section class="container">
    <div class="govuk-width-container">
      <div class="govuk-grid-row">
        <div class="govuk-grid-column-two-thirds">
          <div 
            v-if="invalid" 
            class="govuk-error-summary" 
            aria-labelledby="error-summary-title" 
            role="alert" 
            tabindex="-1" 
            data-module="error-summary">
            <h2 id="error-summary-title" class="govuk-error-summary__title">
              There is a problem
            </h2>
            <div class="govuk-error-summary__body">
              <ul class="govuk-list govuk-error-summary__list">
                <li>
                  <a href="#when-did-you-qualify-error">Select one of the options</a>
                </li>
              </ul>
            </div>
          </div>
          <div>
            <form 
              id="subjects-taught-form"
              action="/validator/subjects-taught">
              <div
                :class="{'govuk-form-group--error': invalid}"
                class="govuk-form-group">
                <fieldset 
                  class="govuk-fieldset govuk-form-group">
                  <input id="school" :value="schoolId" hidden="true" name="schoolId">
                  <legend class="govuk-fieldset__legend govuk-fieldset__legend--xl">
                    <h1 class="govuk-fieldset__heading">
                      The subjects you've taught
                    </h1>
                  </legend>
                  <p class="govuk-body">
                    You can only claim your student loan payments back if you've been teaching one or more of these subjects since 6 April 2018:
                  </p>
                  <ul class="govuk-list govuk-list--bullet">
                    <li>biology</li>
                    <li>chemistry</li>
                    <li>physics</li>
                    <li>computer science</li>
                    <li>languages (not including English)</li>
                  </ul>
                  <p class="govuk-body">
                    <span>
                      Since 6 April 2018, have you taught one or more of these subjects at {{ schoolName }}?
                    </span>
                  </p>
                  <p class="govuk-body">
                    <span class="hint">
                      If you've been off on long-term leave or sick, include the time you were scheduled to teach these subjects.
                    </span>
                  </p>
                  <span v-if="invalid" id="taught-error" class="govuk-error-message">
                    Select one of the options
                  </span>
                  <div class="govuk-radios">
                    <div class="govuk-radios__item">
                      <input 
                        id="taught1" 
                        v-model="checkedNames" 
                        :class="{ 'govuk-input--error': invalid }"
                        class="govuk-radios__input" 
                        name="taught" 
                        type="radio" 
                        value="1"
                        tabindex="4">
                      <label 
                        class="govuk-label govuk-radios__label" 
                        for="taught1">
                        Yes, for more than 50% of your teaching time
                      </label>
                    </div>
                    <div class="govuk-radios__item">
                      <input 
                        id="taught2" 
                        v-model="checkedNames" 
                        :class="{ 'govuk-input--error': invalid }"
                        class="govuk-radios__input" 
                        name="taught" 
                        type="radio" 
                        value="2"
                        tabindex="5">
                      <label 
                        class="govuk-label govuk-radios__label" 
                        for="taught2">
                        Yes, for less than 50% of your teaching time
                      </label>
                    </div>
                    <div class="govuk-radios__item">
                      <input 
                        id="taught3" 
                        v-model="checkedNames" 
                        :class="{ 'govuk-input--error': invalid }"
                        class="govuk-radios__input" 
                        name="taught" 
                        type="radio" 
                        value="3"
                        tabindex="6">
                      <label 
                        class="govuk-label govuk-radios__label" 
                        for="taught3">
                        No, you did not teach any of these subjects
                      </label>
                    </div>
                  </div>
                </fieldset>
              </div>
              <button 
                type="submit"
                class="govuk-button"
                tabindex="7">
                Continue
              </button>
            </form> 
          </div>
        </div>
  </div></div></section>
</template>
<script>
import axios from 'axios'
export default {
  watchQuery: true,
  head: {
    title: 'The subjects you taught'
  },
  async asyncData({ route }) {
    let routeSchoolName = ''
    let error = false
    if (route.query.invalid) {
      error = true
    }

    if (route.query.schoolId) {
      await axios
        .get(`/api/Schools/${route.query.schoolId}`)
        .then(res => {
          routeSchoolName = res.data.name
        })
        .catch(err => {
          console.log(err)
        })
    }

    return {
      invalid: error,
      schoolName: routeSchoolName,
      schoolId: route.query.schoolId
    }
  },
  data: function() {
    return {
      checkedNames: [],
      schoolName: '',
      invalid: false,
      schoolId: ''
    }
  }
}
</script>
<style>
.hint {
  color: #6f777b;
}
</style>
