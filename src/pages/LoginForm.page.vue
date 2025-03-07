<template>

  <n-card>
    <n-tabs
      class="card-tabs"
      default-value="signin"
      size="large"
      animated
      pane-wrapper-style="margin: 0 -4px"
      pane-style="padding-left: 4px; padding-right: 4px; box-sizing: border-box;"
    >
      <n-tab-pane name="signin" tab="Connexion">
        <n-form>
          <n-form-item-row label="Email">
            <n-input />
          </n-form-item-row>
          <n-form-item-row label="Mot de passe">
            <n-input />
          </n-form-item-row>
        </n-form>
        <n-button type="primary" block secondary strong>
          Connexion
        </n-button>
      </n-tab-pane>
      <n-tab-pane name="signup" tab="Inscription">
        <n-form>
          <n-form-item-row label="Email">
            <n-input />
          </n-form-item-row>
          <n-form-item-row label="Mot de passe">
            <n-input />
          </n-form-item-row>
          <n-form-item-row label="Confirmer votre  mot de passe">
            <n-input />
          </n-form-item-row>
        </n-form>
        <n-button type="primary" block secondary strong>
          Inscription
        </n-button>
      </n-tab-pane>
    </n-tabs>
  </n-card>
</template>

<style scoped>
.card-tabs .n-tabs-nav--bar-type {
  padding-left: 4px;
}
</style>