<App>
  <View main>
    <Page>
      <Navbar title="Action Sheet" />
      <Block strong>
        <p class="row">
          <!-- One group, open by direct accessing instance .open() method -->
          <Button class="col" raised onClick={() => actionsOneGroup.open()}>One group</Button>
          <!--  Two groups, open by "actionsOpen" attribute -->
          <Button class="col" raised actionsOpen="#actions-two-groups">Two groups</Button>
        </p>
        <p>
          <!-- Actions Grid, open by changing actionGridOpened state property -->
          <Button raised onClick={() => actionGridOpened = true}>Action Grid</Button>
        </p>
      </Block>

      <BlockTitle>Action Sheet To Popover</BlockTitle>
      <Block strong>
        <p bind:this={buttonToPopoverWrapper}>
          Action Sheet can be automatically converted to Popover (for tablets). This button will open Popover on tablets and Action Sheet on phones:
          <Button
            style="display: inline-block"
            class="button-to-popover"
            onClick={openActionsPopover}
          >
            Actions
          </Button>
        </p>
      </Block>

      <!-- One Group -->
      <Actions bind:this={actionsOneGroup}>
        <ActionsGroup>
          <ActionsLabel>Do something</ActionsLabel>
          <ActionsButton bold>Button 1</ActionsButton>
          <ActionsButton>Button 2</ActionsButton>
          <ActionsButton color="red">Cancel</ActionsButton>
        </ActionsGroup>
      </Actions>

      <!-- Two Groups -->
      <Actions id="actions-two-groups">
        <ActionsGroup>
          <ActionsLabel>Do something</ActionsLabel>
          <ActionsButton bold>Button 1</ActionsButton>
          <ActionsButton>Button 2</ActionsButton>
        </ActionsGroup>
        <ActionsGroup>
          <ActionsButton color="red">Cancel</ActionsButton>
        </ActionsGroup>
      </Actions>

      <!-- Grid -->
      <Actions grid={true} opened={actionGridOpened} onActionsClosed={() => actionGridOpened = false}>
        <ActionsGroup>
          <ActionsButton>
            <img slot="media" src="https://cdn.framework7.io/placeholder/people-96x96-1.jpg" width="48"/>
            <span>Button 1</span>
          </ActionsButton>
          <ActionsButton>
            <img slot="media" src="https://cdn.framework7.io/placeholder/people-96x96-2.jpg" width="48"/>
            <span>Button 2</span>
          </ActionsButton>
          <ActionsButton>
            <img slot="media" src="https://cdn.framework7.io/placeholder/people-96x96-3.jpg" width="48"/>
            <span>Button 3</span>
          </ActionsButton>
        </ActionsGroup>
        <ActionsGroup>
          <ActionsButton>
            <img slot="media" src="https://cdn.framework7.io/placeholder/fashion-96x96-4.jpg" width="48"/>
            <span>Button 4</span>
          </ActionsButton>
          <ActionsButton>
            <img slot="media" src="https://cdn.framework7.io/placeholder/fashion-96x96-5.jpg" width="48"/>
            <span>Button 5</span>
          </ActionsButton>
          <ActionsButton>
            <img slot="media" src="https://cdn.framework7.io/placeholder/fashion-96x96-6.jpg" width="48"/>
            <span>Button 6</span>
          </ActionsButton>
        </ActionsGroup>
      </Actions>
    </Page>
  </View>
</App>
<script>
  import { onDestroy } from 'svelte';
  import { f7, App, View, Page, Navbar, Block, BlockTitle, Button, Actions, ActionsGroup, ActionsLabel, ActionsButton } from 'framework7-svelte';

  let actionGridOpened = false;
  let actionsOneGroup;
  let actionsToPopover = null;
  let buttonToPopoverWrapper;

  onDestroy(() => {
    if (actionsToPopover) {
      actionsToPopover.destroy();
    }
  })

  function openActionsPopover() {
    if (!actionsToPopover) {
      actionsToPopover = f7.actions.create({
        buttons: [
          {
            text: 'Do something',
            label: true,
          },
          {
            text: 'Button 1',
            bold: true,
          },
          {
            text: 'Button 2',
          },
          {
            text: 'Cancel',
            color: 'red',
          },
        ],
        // Need to specify popover target
        targetEl: buttonToPopoverWrapper.querySelector('.button-to-popover'),
      });
    }

    // Open
    actionsToPopover.open();
  }

</script>
