<template>
  <div class="govuk-grid-row">
    <div class="govuk-grid-column-two-thirds">
      <div class="govuk-heading-xl">
        You're eligible to claim your student loan payments
      </div>
      <p class="govuk-body">
        Based on your answers, you are eligible to claim your student loan payments back.
      </p>
      <p class="govuk-body">
        You can apply from September 2019. Register your details and we'll send you updates about the service.
      </p>
      <a href="https://goo.gl/forms/4c8YAvjY3eDqOqdk1" role="button" draggable="false" class="govuk-button" tabindex="4">
        Register for updates
      </a>
      <p class="govuk-body">
        If you've worked at another school since 6 April 2018 
        <nuxt-link to="/" role="button" draggable="false" tabindex="5">
          check your eligibility again.
        </nuxt-link>
      </p>
    </div>
  </div>
</template>

<script>
export default {
  head: {
    title: 'You are eligible'
  }
}
</script>
