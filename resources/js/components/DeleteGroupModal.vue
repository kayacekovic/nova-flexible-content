<template>
    <Modal :show="true">
    <form
      @submit.prevent="$emit('confirm')"
      class="mx-auto bg-white dark:bg-gray-800 rounded-lg shadow-lg overflow-hidden"
    >
      <slot>
        <ModalHeader v-text="__('Delete Group')" />
        <ModalContent>
            <p class="leading-normal" v-if="!deletable && unableToDeleteMessage">
                {{ unableToDeleteMessage }}
            </p>
            <p class="leading-normal" v-else-if="!deletable">
                {{ __('Unable to delete the group, you are not authorized') }}
            </p>
            <p class="leading-normal" v-else-if="message">
                {{ message }}
            </p>
            <p class="leading-normal" v-else>
                {{ __('Are you sure you want to delete this group?') }}
            </p>
        </ModalContent>
      </slot>

      <ModalFooter>
        <div class="ml-auto">
          <link-button
            type="button"
            data-testid="cancel-button"
            dusk="cancel-delete-button"
            @click.prevent="this.$emit('close')"
            class="mr-3"
          >
            {{ no }}
          </link-button>

          <danger-button
            ref="confirmButton"
            dusk="confirm-delete-button"
            :processing="working"
            :disabled="working || !deletable"
            type="submit"
          >
            {{ yes }}
          </danger-button>
        </div>
      </ModalFooter>
    </form>
    </Modal>
</template>

<script>
export default {
    props: ['message', 'yes', 'no', 'deletable', 'unableToDeleteMessage'],

    emits: ['close', 'confirm'],

    /**
     * Mount the component.
     */
    mounted() {
        this.$nextTick(() => {
            // this.$refs.confirmButton.button.focus()
        })
    },
}
</script>
