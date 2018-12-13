# Django Admin Totals

Module to show totals in Django Admin List.

## Installation

    virtualenv .
    source bin/activate
    pip install git+https://github.com/somghosh/admin-totals.git
    
    This was forked from original repo and maintained by Sam given the original repo is not that well maintained, and didnt want new changes to break our production code

## Usagge

In settings.py

    INSTALLED_APPS = [
        'admin_totals',
    ]

In admin.py:

    from admin_totals.admin import ModelAdminTotals
    from django.contrib import admin
    from django.db.models import Sum, Avg
    from django.db.models.functions import Coalesce

    @admin.register(MyModel)
    class MyModelAdmin(ModelAdminTotals):
        list_display = ['col_a', 'col_b', 'col_c']
        list_totals = [('col_b', lambda field: Coalesce(Sum(field), 0))), ('col_c', Avg)]

Make sure to at least have the columns of `list_totals` in `list_display`.
