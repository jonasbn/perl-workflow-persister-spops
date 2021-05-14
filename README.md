# NAME

Workflow::Persister::SPOPS - Persist workflows using SPOPS

# VERSION

This documentation describes version 1.53 of this package

# SYNOPSIS

    <persister name="SPOPSPersister"
               class="Workflow::Persister::SPOPS"
               workflow_class="My::Persist::Workflow"
               history_class="My::Persist::History"/>

# DESCRIPTION

## Overview

Use a SPOPS classes to persist your workflow and workflow history
information. Configuration is simple: just specify the class names and
everything else is done.

We do not perform any class initialization, so somewhere in your
server/process startup code you should have something like:

    my $config = get_workflow_and_history_config();
    SPOPS::Initialize->process({ config => $config });

This will generate the classes named in the persister configuration.

## SPOPS Configuration

**NOTE**: The configuration for your workflow history object **must**
use the [SPOPS::Tool::DateConvert](https://metacpan.org/pod/SPOPS%3A%3ATool%3A%3ADateConvert) to translate the 'history\_date'
field into a [DateTime](https://metacpan.org/pod/DateTime) object. We assume when we fetch the history
object that this has already been done.

## METHODS

### init ( \\%params)

This method initializes the SPOPS persistance entity.

It requires that a workflow\_class and a history\_class are specified. If not the
case [Workflow::Exception](https://metacpan.org/pod/Workflow%3A%3AException)s are thrown.

### create\_workflow

Serializes a workflow into the persistance entity configured by our workflow.

Takes a single parameter: a workflow object

Returns a single value, a id for unique identification of out serialized
workflow for possible deserialization.

### fetch\_workflow

Deserializes a workflow from the persistance entity configured by our workflow.

Takes a single parameter: the unique id assigned to our workflow upon
serialization (see ["create\_workflow"](#create_workflow)).

Returns a hashref consisting of two keys:

- state, the workflows current state
- last\_update, date indicating last update

### update\_workflow

Updates a serialized workflow in the persistance entity configured by our
workflow.

Takes a single parameter: a workflow object

Returns: Nothing

### create\_history

Serializes history records associated with a workflow object

Takes two parameters: a workflow object and an array of workflow history objects

Returns: provided array of workflow history objects upon success

### fetch\_history

Deserializes history records associated with a workflow object

Takes a single parameter: a workflow object

Returns an array of workflow history objects upon success

# SEE ALSO

- [Workflow::Persister](https://metacpan.org/pod/Workflow%3A%3APersister)
- [SPOPS](https://metacpan.org/pod/SPOPS)
- [SPOPS::Tool::DateConvert](https://metacpan.org/pod/SPOPS%3A%3ATool%3A%3ADateConvert)

# COPYRIGHT

Copyright (c) 2003-2021 Chris Winters. All rights reserved.

This library is free software; you can redistribute it and/or modify
it under the same terms as Perl itself.

Please see the `LICENSE`

# AUTHORS

Please see [Workflow](https://metacpan.org/pod/Workflow)
