# Boostrap modal form ajax handler

Using this library, you can easily:

 * Create **ajax based modal forms**
 * Display **modal confirmations** with custom messages
 * Load modal content dynamically

This library depends on [Bootstrap](http://getbootstrap.com/) ~3.3, [Bootstrap modal library](http://getbootstrap.com/javascript/#modals) and [jQuery](http://jquery.com/) > 1.9.

## Installiation

You can install this library using Bower:

    bower install bootstrap-modal-form

Or download latest release from GitHub:

    https://github.com/DATA-DOG/bootstrap-modal-form/archive/master.zip

*Do not forget to load downloaded script into your webpage!*

## Usage

* To load modal using ajax, simply add class `.js-modal` and provide `data-url` tag for any element.

  Example:

      <a href="#" data-url="/myModalContent" class="js-modal">Open Modal</a>

  `/myModalContent` should return status code 200, with modal content. Example response template:

      <div class="modal-header">
        <button type="button" class="close" data-dismiss="modal" aria-label="Close">
          <span aria-hidden="true">&times;</span>
        </button>
        <h4 class="modal-title">Test Modal</h4>
      </div>

      <div class="modal-body">
        <form action="/formAction" method="post" class="js-form">
          <input type="text" name="test">

          <button type="submit" class="btn btn-primary">
            Submit
          </button>
          <button type="button" class="btn btn-default" data-dismiss="modal">
            Cancel
          </button>
        </form>
      </div>

  To submit forms and display result in same modal, just add `.js-form` class to your form! It's that simple. Returned template (from `/formAction`) should include handled form, with all errors rendered.

  If you want to redirect user after form submit, return response with status code 201 and body:

      {"redirect": "http://myRedirectLink.com"}

* To display confirmation modals, just add `.js-confirm` to any element, and optionally provide `data-title` (for title), and `data-text` (for modal content) attributes.

  Example:

      <a href="/update" data-text="Do you want to update?" data-title="Update member #1">
        Update
      </a>

  Confirming modal will send AJAX request to element href, if you do not want that (you need a redirect), add `.js-no-ajax` class to that element.

## Overwriting templates

This library injects default templates. If you want to customize them, add following elements to `body`, and change them for your needs.

    <div id="bsModalContent" class="hidden">
      <div class="modal-body">
        Loading...
      </div>
    </div>

    <div id="bsModalConfirmContent" class="hidden">
      <div class="modal-header">
        <button type="button" class="close" data-dismiss="modal" aria-label="Close">
          <span aria-hidden="true">&times;</span>
        </button>
        <h4 class="classic-title" id="bsModalTitle"></h4>
      </div>
      <div class="modal-body"></div>
    </div>

    <div id="bsModalConfirmButtons" class="hidden">
      <div class="clearfix">
        <button class="btn-system btn-large js-confirm-btn">Confirm</button>
        <button type="button" class="btn-system btn-large border-btn" data-dismiss="modal">
          Cancel
        </button>
      </div>
    </div>
